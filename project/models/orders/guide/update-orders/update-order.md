---
description: ""
date: "2020 - May - 26"
draft: false
author: sejal.parikh
---

# Update Your Order

Updates the order.

Here's the sample code that you can use to update your order in Java.

```java
URL url = new URL("https://{shortCode}.api.commercecloud.salesforce.com/checkout/orders/{version}/organizations/{organizationId}/orders/{orderNo}");
HttpsURLConnection con = (HttpsURLConnection) url.openConnection();
con.setRequestMethod("PATCH");

/* Payload support */
con.setDoOutput(true);
DataOutputStream out = new DataOutputStream(con.getOutputStream());
out.writeBytes("{\n");
out.writeBytes("  \"c_carrierCode\": \"DHL\",\n");
out.writeBytes("  \"c_review\": null,\n");
out.writeBytes("  \"c_weight\": 2.4\n");
out.writeBytes("}");
out.flush();
out.close();

int status = con.getResponseCode();
BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer content = new StringBuffer();
while((inputLine = in.readLine()) != null) {
	content.append(inputLine);
}
in.close();
con.disconnect();
System.out.println("Response status: " + status);
System.out.println(content.toString());
```
