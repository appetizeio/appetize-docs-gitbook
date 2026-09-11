# Access Rules

Control who can reach your organization by IP address, and which sites can embed your apps.

Both live under **Organization → Access Rules** at [appetize.io/organization/access-rules](https://appetize.io/organization/access-rules), on two tabs:

| Tab               | Controls                                        | Plan       |
| ----------------- | ----------------------------------------------- | ---------- |
| **IP Access**     | Which IP addresses can sign in and run sessions | Enterprise |
| **Embed Domains** | Which sites can embed your apps                 | All plans  |

Any team member with the developer role can view this page. Only **admins** can add, edit or delete.

## IP Access

An IP access rule is a list of IPv4 addresses or CIDR ranges, labelled, and marked either **Allow** or **Deny**.

{% embed url="https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FfPzIAMV4GgsDPYIl9MZD%2Faccess-rules-ip.mp4?alt=media&token=a9ef5f29-1451-4ce4-9458-d568729d3dad" %}





### How a request is evaluated

Only rules you have applied to the organization are evaluated. Among those, the order is:

1. **Deny always wins.** If the IP matches any deny rule, the request is blocked — even if an allow rule also matches it.
2. **If any allow rule exists, the IP must match one.** Anything not on an allow list is blocked.
3. **If no allow rules exist,** every IP is allowed except those explicitly denied.

So a single applied allow rule switches the organization from "open to everyone" to "open to this list only".

### Applying a rule

Saving a rule does not enforce it. Each rule has an **Apply to my organization** toggle, and only applied rules are evaluated — so you can write a rule, check it reads the way you meant, and turn it on separately.

To stop enforcing a rule without losing it, edit it and turn that toggle off. Deleting is only for rules you no longer want at all.

Appetize will not let you lock yourself out: if saving or applying a rule would block the address you are currently on, the save is rejected with _"This change would block your current IP … from accessing this account."_ Add your own address to an allow list first, then apply.

{% hint style="warning" %}
That check only covers **your** address at the moment you save. It cannot know about teammates on other networks, or your own address changing later — so list every range your team connects from before you apply an allow rule.
{% endhint %}

### What the rules apply to

Rules are checked on **authenticated user actions**: signing in, loading the dashboard, starting and running sessions.

They do **not** apply to:

* **API token requests.** Automation keeps working from anywhere, so CI runners do not have to be allowlisted.

### Accepted values

| Value                                               | Example                         |
| --------------------------------------------------- | ------------------------------- |
| A single IPv4 address                               | `203.0.113.10`                  |
| A CIDR range                                        | `203.0.113.0/24`                |
| Several of either, separated by commas or new lines | `203.0.113.10, 198.51.100.0/24` |

IPv6 is not supported. Decimal-integer forms of an address (`3405803786`) are rejected — use dotted quads.

### When someone is blocked

They land on an **Access Denied** page naming the blocked IP, and are told to contact an account admin. The request itself fails with `403` and the message `IP address <ip> not allowed`.

Blocked sign-ins are recorded in [Audit Events](https://appetize.io/organization/audit-events), which is the place to look when someone reports they cannot get in.

## Embed Domains

By default your apps can be embedded on any site. Adding a domain here restricts embedding to the domains you list.

Appetize matches the hostname of the browser's `Referer` header against your list. Wildcards are supported, so `*.example.com` covers `docs.example.com` and `app.example.com`.

| Entry           | Matches                          |
| --------------- | -------------------------------- |
| `example.com`   | that hostname exactly            |
| `*.example.com` | any single-level subdomain of it |

Enter hostnames only — no scheme, port or path. An empty list means no restriction at all.

{% embed url="https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FoRO1HXWcCEozlw9hsLD2%2Faccess-rules-domains.mp4?alt=media&token=949d23c2-f87a-46eb-b153-542423c399cb" %}

### Requests with no Referer

Some browsers and privacy tools strip the `Referer` header, and a request without one cannot be matched against your list. The **If Referer is not provided** toggle decides what happens then:

* **Allow** — requests with no Referer are let through. Fewer false blocks, weaker restriction.
* **Deny** — only requests carrying a matching Referer are allowed. Stricter, and will block some legitimate visitors.

The toggle appears once you have added at least one domain.
