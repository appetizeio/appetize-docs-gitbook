# List apps

## Apps

{% hint style="info" %}
The returned app(s) will display only explicitly set parameters, with all other values defaulting to the organization or Appetize defaults.
{% endhint %}

{% swagger src="../.gitbook/assets/appetize-v1 (1).yaml" path="/apps" method="get" %}
[appetize-v1 (1).yaml](<../.gitbook/assets/appetize-v1 (1).yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/appetize-v1 (1).yaml" path="/apps/all" method="get" %}
[appetize-v1 (1).yaml](<../.gitbook/assets/appetize-v1 (1).yaml>)
{% endswagger %}

{% swagger src="../.gitbook/assets/appetize-v1 (1).yaml" path="/apps/{app_publicKey}" method="get" %}
[appetize-v1 (1).yaml](<../.gitbook/assets/appetize-v1 (1).yaml>)
{% endswagger %}

## App Groups

{% swagger src="../.gitbook/assets/appetize-v1 (1).yaml" path="/apps/{appgroup_publicKey}" method="get" %}
[appetize-v1 (1).yaml](<../.gitbook/assets/appetize-v1 (1).yaml>)
{% endswagger %}
