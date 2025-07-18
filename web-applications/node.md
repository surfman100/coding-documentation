# Node & NPM
Hints & tips on using Node & NPM

## SSL error
To get around that annoying error behind corporate firewall try

`set NODE_TLS_REJECT_UNAUTHORIZED=0`  
`npm set strict-ssl false`

although a better approach is recommended here
[Node and SSL certs](https://stackoverflow.com/questions/13913941/how-to-fix-ssl-certificate-error-when-running-npm-on-windows)
