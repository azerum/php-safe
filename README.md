Initial sketch for running `php` and `composer` in macOS sandbox. 
Inspired by [node-safe](https://github.com/berstend/node-safe)

# Why?

Currently, when you install some composer package, use it in your code,
and run PHP locally, you execute the third-party code on your computer.
The code is unrestricted, and has the same permissions as your current user. 
The code hence can do any of these things:

- Read you SSH key in ~/ssh and send it to evil server on the web
- Do the same with any file you can open
- Wipe all the files you have access to, as [node-ipc did](https://snyk.io/blog/peacenotwar-malicious-npm-node-ipc-package-vulnerability/)*
- Modify executable to inject malicious code

> * - I fully support Ukraine in the ongoing conflict. node-ipc is a good example of what
> dependencies of your dependencies your don't even know about can do

# Usage

```
./sb php -S localhost:8080
./sb composer install
./sb echo "Actually, any command can be run in this sandbox" > indeed.txt
```

# This is a sketch(!)

Current version **does** protect you from:

[x] Accessing any files outside current directory (where ./sb is run).
This prevents SSH key theft, wiping your desktop, stealing your ingenious-plans.txt

However, it **doesn't** protect your from:

- Wiping the entire contents of *current* directory (e.g. all your local copy of repository)
- Accessing the Internet. Combined with previous one, your private source code can be stolen

It might be that due to complexity of sneaking into composer registry with malicios code,
the above scenarious are not really worth the effort for the attacker. But keep these limitation
in mind

# Contribution

macOS sandbox profiles are written in TinyScheme. There's a [great PDF](https://reverse.put.as/wp-content/uploads/2011/09/Apple-Sandbox-Guide-v1.0.pdf) 
explaining the format
