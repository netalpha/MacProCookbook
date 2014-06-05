# Use in Another Computer

Sometimes, we need to work outside in another computer. So we can just `git clone` your codes to the working computer.

###### Step 1: Prepare Your Code

``` sh
$ git clone git@bitbucket.org:username/your_blog_code.git some_name
# git clone your source code

$ cd some_name
# switch to that directory

$ git clone git@github.com:username/username.github.com.git _deploy
# because octopress use _deploy folder to publish your blog
```

###### Step 2: Publish Your Post

``` sh
$ rake generate
# generate static blog files to public folder

$ rake deploy
# copy the files in public folder into _deploy and publish to github
```

That's it!
