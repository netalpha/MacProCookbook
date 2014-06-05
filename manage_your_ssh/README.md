# Manage Your SSH

## Set Up New Multiple Git Accounts with SSH Config

### GitHub Account 1

###### Step 1: SSH-Keygen for Account 1

``` sh
$ ssh-keygen -f github_account1
```

###### Step 2: Add It to SSH Config

- If using `ssh` to connect to GitHub, add as follows:

``` sh
Host github.com
  Hostname github.com
  IdentityFile ~/.ssh/github_account1
  PreferredAuthentications publickey
  port 22
```

- If using `https` to connect to GitHub, add as follows:

``` sh
Host github.com
  Hostname ssh.github.com
  IdentityFile ~/.ssh/github_account1
  PreferredAuthentications publickey
  port 443
```

###### Step 3: Add the Key to GitHub

``` sh
$ pbcopy < ~/.ssh/github_account1.pub
# Copies the contents of the github_account1.pub file to your clipboard
```

Go to [SSH Keys](https://github.com/settings/ssh) of your Github [Account Settings][2] and paste your key into the `Key` field.

### GitHub Account 2

###### Step 1: SSH-Keygen for Account 2

``` sh
$ ssh-keygen -f github_account2
```

###### Step 2: Add It to SSH Config

- If using `ssh` to connect to GitHub, add as follows:

``` sh
Host github_account2.com
  Hostname github.com
  IdentityFile ~/.ssh/github_account2
  PreferredAuthentications publickey
  port 22
```

- If using `https` to connect to GitHub, add as follows:

``` sh
Host github.com
  Hostname ssh.github.com
  IdentityFile ~/.ssh/github_account2
  PreferredAuthentications publickey
  port 443
```

###### Step 3: Add the Key to GitHub

``` sh
$ pbcopy < ~/.ssh/github_account2.pub
# Copies the contents of the github_account2.pub file to your clipboard
```

Go to [SSH Keys][1] of your Github [Account Settings][2] and paste your key into the `Key` field.

###### Step 4: Set Remote URL to the Local Repository (Important)

The default remote pointer `origin` is with url `github.com`. It will try to find the default `ssh` configuration (here account 1) when you try to push your code. Since you have different GitHub accounts, you should tell your local repository to connect to the corespondent GitHub account as follows:

```sh
$ git remote set-url origin git@github_account2.com:yourusername/test.git
```

### Heroku Account

###### Step 1: SSH-Keygen

``` sh
$ ssh-keygen -f heroku
```

###### Step 2: Add the Key to Heroku

``` sh
$ heroku login
# it will prompt when you have multi-keys.
```

###### Step 3: Find the IP Which Can Be Connected (for Chinese Users)

Temporally add `~/.ssh/config` as follow:

```sh
Host heroku.com
  Hostname proxy.heroku.com
  IdentityFile ~/.ssh/heroku
  PreferredAuthentications publickey
  port 22
```

``` sh
$ ssh -v git@heroku.com
```

You will get a useful IP like `107.21.95.3`.

Modify again

``` sh
Host heroku.com
  Hostname 107.21.95.3
  IdentityFile ~/.ssh/heroku
  PreferredAuthentications publickey
  port 22
```


### Test and Tools

###### Test the Connection
``` sh
$ ssh -T git@github.com
# Attempts to ssh to Github_Account1

$ ssh -T git@github_account2.com
# Attempts to ssh to GitHub_Account2
```

###### Heroku SSH Key Management

``` sh
$ heroku keys:clear
# remove all the authentication keys
```

## Use Existing SSH Config Repo

I don't want to bother myself each time when I reinstall my computer or set up a new computer. So I just store my SSH config files to a private repository (which can only be seen by myself). My ssh config repository looks like this:

``` sh
.
├── README.md
├── bitbucket
├── bitbucket.pub
├── config -> config_ssh
├── config_https
├── config_ssh
├── github_chavez
├── github_chavez.pub
├── github_rsa
├── github_rsa.pub
├── heroku
├── heroku.pub
└── known_hosts
```

###### Step 1: Clone the Ssh Config Repo

```sh
> git clone git@github.com:username/repo_name.git
```

###### Step 2: Link to main config

- If I choose to use `ssh` to connect to a git repo,

```sh
> ln -s config_ssh config
```

- If I choose to use `https` to connect to a git repo,

```sh
> ln -s config_https config
```

###### Troubleshooting

If failed to push code to remote repo, you should:

```sh
> chmod 700 config_ssh
> chmod 700 config_https
```

That's it for my ssh management! You can add anything you want by yourself.

[2]: https://github.com/settings

