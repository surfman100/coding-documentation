## API Development
Looks reasonable to version API's in the URL
e.g.

`
{HTTP method} https://graph.microsoft.com/{version}/{resource}?{query-parameters}
`

e.g. the version could be *v1.0* or *beta*

Use Pagination for large data requests. In Microsoft Graph, this is done using @odata.nextLink
