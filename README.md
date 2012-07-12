# Push2heroku

Makes it easy to push to heroku.

## Installation

Add this to Gemfile:

    gem 'push2heroku'

## Usage

After installing the gem copy [this file](https://raw.github.com/gist/3098161/578dad8cd3933834712a8afdf33520221dbdb986/push2heroku.yml) to `config/push2heroku.yml` .

Change the contents of `config/push2heroku.yml` as per your needs after
reading rest of README.

## What problem it solves

Here at BigBinary we create a separate branch for each feature we work
on. Let's say that I am working on `authentication with facebook`.
When I am done with the feature then I send pull request to my team
members to review. However in order to review the work all the team
members need to pull down the branch and fire up `rails server` and then
review.

We like to see things working. So we developed `push2heroku` to push a
feature branch to heroku instantly with one command. Executing
`push2heroku` prints a url and we put that url in the pull request so
that team members can actually test the feature.

## Here is how it works

`push2heroku` reads the `push2heroku.yml` and executes those commands.
It's that simple.

Lets say that I am working in a branch called
`76-facebook-authentication`. When I execute `push2heroku` then the
application name under which it will be deployed to heroku will be
`nimbleshop-76-facebook-neeraj`.

`nimbleshop` is the name of the project.
`76-facebook` is the first 10 letters of the branch name.
`neeraj` is the first 5 letters of my github user name.

So in this case the url of the application will be
`http://nimbleshop-76-facebook-neeraj.herokuapp.com` .

In the `push2heroku.yml` file the keys `production` and `staging`
are branch names. And these branches are special branches. For these
branches the url generated will be just the application name and the
branch name. For example if I execute `rake push2heroku` from `staging`
branch then the heroku url will be
`http://nimbleshop-staging.herokuapp.com`.

However if I delete `staging` key from `push2heroku.yml` then `staging`
is no longer a special branch and the heroku url would be
`http://nimbleshop-staging-neeraj.herokuapp.com` .

## Resetting the database

When the application is deployed for the very first time then you want
the database to reset and some sort of setup to be run. However on
subsequest deployment you do not need to run those setup tasks.

To incorporate that on first deployment `push2heroku` will execute
commands mentioned under key `hard`. Here `hard` stands for hard push.
Subsequent pushes will be `soft` push.

If you want to force `hard` push anytime then execute `rake push2heroku
HARD=true`.

## License

`push2heroku` is released under MIT License.
