---
description: How is the repository built and hosted?
---

# Infrastructure

## The idea

The whole thing started while trying to package a tool that wasn't part of the official Solus-Project: it was back then I found out the work done by [Devil505](https://gitlab.com/devil505).

{% embed url="https://gitlab.com/devil505/solus-3rd-party-repo" %}

He basically had done what I wanted in a slightly messier way, but the idea behind the project was the same I had: collecting packages that the Solus-Project would have not included in the official repository, all the while in a single Git repository.

### Git repository structure standardization

The first thing I reorganized has been the physical repository file organization, hence the choice to move all the packages templates in a dedicated `src` folder and drop all the `eopkg` \(the effective package files\).

The main reason to drop out all the `eopkg` files was about the fact it could have lead to a very massive repository and Git has not been built to host binary files. On the other hand, GitHub is offering the _Releases_ functionality which is actually more about file hosting \(and projects releases, indeed\), so I preferred to differentiate roles: the repository keeps all the packages `yml` templates, the instructions needed to build them, while the _Releases_ wraps all the history of repository's packages updates.

### Incremental and automated building

My repository offers a `Makefile` to batch _do things_, such as doing a common repository full build or check for packages pending updates.

The order used by the `Makefile` to build files is imposed by the `src/series` file: this is needed as several packages have build dependencies _inside_ the repository itself. Hence, the `series` file split all the packages in iteration groups, which assure that a specific `package-x` gets built and indexed on the local \(in-build\) repository before the depending `package-y` package.

Also, in order to make the whole process work, the local build directory needs to be set as local repository to `solbuild` \(the tool used to build the package starting from a `package.yml` template\). This can be done editing the `/usr/share/solbuild/main-x86_64.profile` profile settings and adding the following lines:

{% code-tabs %}
{% code-tabs-item title="main-x86\_64.profile" %}
```text
[repo.local-build-repository]
uri = "/path/to/ashtray/bin"
local = true
autoindex = true
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Packages \(free\) hosting

This section resumes what was outlined in the [About page](about.md#installation).

Basically, the whole Solus-Project repository is hosted on GitHub: the packages templates and build instructions in the Git repository itself, while the built `eopkg` files and the indexes are kept in dedicated repository releases.

The issue I faced were:

1. the repository URL was way too long and complicated to be easily remembered
2. `eopkg` repository management does not support repository URL redirections: this means `github.com/streambinder/ashtray/releases/latest` could not be given and that the only way to offer the repository without additional headaches was to create a single fixed release, which would have been filled with any package updates everytime it was needed.

These two issues lead to the additional headache of configuring a custom web server which translates the requests made to `https://solus.davidepucci.it` to the latest GitHub repository release, by rewriting the request `Location` header. This gets done with this little PHP snippet:

```php
<?php
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, 'https://github.com/streambinder/ashtray/releases/latest');
    curl_setopt($ch, CURLOPT_HEADER, true);
    curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_exec($ch);
    $ch_url = curl_getinfo($ch, CURLINFO_EFFECTIVE_URL);
    $ch_download_url = str_replace('/tag/', '/download/', $ch_url);
    header("location: ".$ch_download_url.$_SERVER['REQUEST_URI']);
?>
```

This way, the `solus.davidepucci.it` host behaves as a poor proxy redirecting dynamically the requests without taking charge of the traffic of repository indexes and packages downloads.

Also, this `.htaccess` is used to forward all the files `GET`requests to the PHP snippet above:

{% code-tabs %}
{% code-tabs-item title=".htaccess" %}
```text
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^.*$ /index.php [L,QSA]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

