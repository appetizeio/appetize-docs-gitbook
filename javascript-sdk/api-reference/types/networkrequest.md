# NetworkRequest

| Property        | Type                                                                                                                                                    |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | 'request'                                                                                                                                               |
| serverIPAddress | string                                                                                                                                                  |
| requestId       | string                                                                                                                                                  |
| request         | { method: string; url: string; httpVersion: string; cookies: string\[]; headers: Array; queryString: string\[]; headersSize: number; bodySize: number } |
| cache           | Record                                                                                                                                                  |
