# GIT Guide & Tips

## Useful GIT Commands

wipe all changes. Will not remove folders by .dotnet, obj etc  
`git reset --hard`

wipe all changes. This should wipe obj/bin folders  
`git clean -xdf --dry-run `

## Configuration
use Nano....wayyyyy easier to get going on  
`git config --global core.editor "nano"`

other options like vscode are possible, see [here](https://salferrarello.com/git-commit-message-editor/)  

## SSL Certificates
if you are having problems with SSL, you can ignore error using:  
`git -c http.sslVerify=false push`

## Learning
the site https://githubtraining.github.io/training-manual is good but a lot of broken links.
