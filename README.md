# Illegal Auth Attempts

This set of scripts aims to extract from auth attempts or device scanning IPs and users used for those auth attempts.

## IPS

The top 10 IPs are:

| IP              | Count |
| --------------- | -----:|
| 103.27.239.2 | 11192 |
| 123.183.209.139 | 10079 |
| 103.99.0.188 | 5760 |
| 61.177.172.64 | 5505 |
| 59.63.166.104 | 5465 |
| 18.217.140.251 | 5064 |
| 59.63.188.32 | 4800 |
| 59.63.188.36 | 4474 |
| 59.63.166.105 | 4045 |
| 123.183.209.140 | 3964 |

## Users

The top 10 users are:

| User    | Count |
| ------- | -----:|
| admin | 4057 |
| test | 2140 |
| user | 2093 |
| guest | 1523 |
| pi | 1079 |
| oracle | 797 |
| ftpuser | 683 |
| postgres | 652 |
| support | 597 |
| ubuntu | 581 |

## Files

If you didn't use the fetch script to get you `IPs.log` and `users.log`, you can put your `auth.log` or `secure` files in `import/sources/` (those files are ignored by git, so it won't be uploaded) - then you have to import them - refer to importing section

If you used the fetch script, put your `IPs.log` and `users.log` files in `import/` and prefix them to distinguish them from other users' files and devices (please only use letters, numbers, dash and underscore in the prefix - I use a githubusername_devicename pattern)

## How and what

### Fetching

The `fetch/fetch.sh` script get from `/var/log/auth.log` the IPs and users of the previous day lines of the log. Hence it has to be run only once a day to get everything and to not duplicate data.

Moreover, for it to work, the cron has to be able to read `/var/log/auth.log` or `/var/log/secure`.

### Importing

If you're fetching IPs and Users on several devices and want to centralize everything on one, you can put your `auth.log` or `secure` files in `import/sources/`.

Please prefix your auth.log or secure files per device in order to distinguish them, I use a githubusername_devicename pattern (only use letters, numbers, dash and underscore in the prefix, or it won't work).

### Counting and sorting

Once enough data gathered, and the `IPs.log` and `users.log` are created in `import/`, the `IAA.sh` will create unique IPs and users lists, as well as lists with count of their occurences in the original logs, sorted descendingly.

### Prerequisites

- An `/var/log/auth.log` (or the fetch script will have to be adaptated to your auth logging)
- Python 3

### Contributing

You can run this script on your public facing devices to collect the IPs and users too, and if you want to contribute, please refer to Import section.
Once you're done, run `./import.sh` if needed, and `./IAA.sh` - commit and then create a pull request.

Note that you will need git lfs for `src/` and `import/`.
