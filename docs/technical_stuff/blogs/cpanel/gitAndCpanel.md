
# How to clone a private Github repo into Cpanel

The goal of this blog post is to help you in setting up your Github private repo on Cpanel, so that when you make a push to your blog post, then those changes are synced automatically. 


<center><img src="../images/header.png" width="100%"></center>

So let's get started 😀

### Generate a key in Cpanel

The goal is the create a public and private key pair. Then copy the public key and save it in Github. First we will create a pair in Cpanel. For this go to `Cpanel` --> `Security` --> `SSH Access` --> `Manage Keys` --> `Generate New Key` (enter a strong password) 

### Copy public key from Cpanel

After generating a public-private key pair, now is the time to copy the public key. For doing this, go to SSH Access --> `Manage SSH Keys` --> `Public keys` -->  `Authorize` (make authorize) --> Go back --> Press `view/download` --> `Download key` --> open it using a text editor and copy it.

### Copy public key to Github

The goal is to save the public key in your private git repo, so that Cpanel can fetch data from it. Go to your `Github` --> Your private repo --> `Settings` --> `Deploy Keys` --> `add deploy key` -->  Provide any title and paste the public key.

### Add an `.cpanel.yml` file.

Before we go ahead, we need to make sure the files we add from the Github are deployed to cpanel. You will need to know 2 important things here

1. `yourUserName/repositories` : this is the folder where all the repo's will get synced.
2. `yourUserName/public_html` : This is the folder from where the actual site content is served. So, this should contain an `index.html` at minimum. 

The `.cpanel.yml` file is a basic configuration file. It can be used to copy the contents from your `yourUserName/repositories/subdir` directory to `yourUserName/public_html` for example.


Make sure you've added a `.cpanel.yml` file at the root of your project that you are uploading. The contents of this file can be something like

```properties
---
deployment:
  tasks:
    - export DEPLOYPATH=/home/ReplaceItByYourUserName/public_html/
    - /bin/rm -Rf $DEPLOYPATH
    - /bin/mkdir $DEPLOYPATH
    - /bin/cp -R FileWhereSiteContentIsLocated/* $DEPLOYPATH
```

### Clone a repo to CPanel

 After you upload your project, this file will be hidden (as this is a . file) but can be seen by going to your directory from cPanel home --> Advanced --> Shell

```sh
cd yourHome/Repositories
ls -a
```

Go to Cpanel --> Git™ Version Control --> create clone url and enter the similar `Clone URL`

```sh
 git@github.com:<user_name>/<repository_name>.git
```

The `Repository Path` and `Repo Name` will be autofilled. Then hit create.

### Pull from the sources.

<center><img src="../images/a.png" width="100%"></center>

Manage repository from list --> `Manage` --> pull or deploy from Github --> Click on `Update from Remote`: works perfectly (any files edit or delete you fetch/pull from GitHub now)

Cheers 🍻

