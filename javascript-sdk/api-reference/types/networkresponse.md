# NetworkResponse

| Property        | Type                                                                                                                                                                                                                                                                                      |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | 'response'                                                                                                                                                                                                                                                                                |
| serverIPAddress | string                                                                                                                                                                                                                                                                                    |
| requestId       | string                                                                                                                                                                                                                                                                                    |
| request         | { method: string; url: string; httpVersion: string; cookies: string\[]; headers: Array; queryString: string\[]; headersSize: number; bodySize: number }                                                                                                                                   |
| response        | { status: number; statusText: string; httpVersion: string; cookies: string\[]; headers: Array; redirectURL: string; headersSize: number; bodySize: number; content: { size: number; mimeType: string; compression: number; text: string }; postData: { mimeType: string; text: string } } |
| cache           | Record\<string, any>                                                                                                                                                                                                                                                                      |