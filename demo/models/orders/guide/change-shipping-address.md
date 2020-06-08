---
description: ""
date: "2020 - May - 26"
draft: false
author: sejal.parikh
---

# Change Your Shipping Address

Use the [Orders API](orders-api-overview.md) to update the shipping address on an existing order.

For example, when a shopper wants to change their shipping address after the order is created.

```c
#include <stdio.h>
#include <curl/curl.h>

int main(void)
{
	CURL *curl;
	CURLcode res;

	curl = curl_easy_init();
	curl_easy_setopt(curl, CURLOPT_URL, "https://{shortCode}.api.commercecloud.salesforce.com/checkout/orders/{version}/organizations/{organizationId}/orders/{orderNo}/shipments/{shipmentId}/shipping-address");
	curl_easy_setopt(curl, CURLOPT_CUSTOMREQUEST, "PUT");
	/* if redirected, tell libcurl to follow redirection */
	curl_easy_setopt(curl, CURLOPT_FOLLOWLOCATION, 1L);


	char *body ="{  \"address1\": \"100 Presidential Way\",  \"address2\": \"100 Presidential Way 2\",  \"c_district\": \"South End\",  \"c_floor\": 2,  \"c_note\": \"Engineering\",  \"city\": \"Woburn\",  \"companyName\": \"DWRE\",  \"countryCode\": \"US\",  \"firstName\": \"John\",  \"jobTitle\": \"Director\",  \"lastName\": \"Smith\",  \"phone\": \"+1 123 456789\",  \"postalCode\": \"01801\",  \"salutation\": \"Mr.\",  \"secondName\": \"Daniel\",  \"stateCode\": \"MA\",  \"title\": \"Prof. Dr.\"}";
	curl_easy_setopt(curl, CURLOPT_POSTFIELDS, body);

	/* Perform the request, res will get the return code */
	res = curl_easy_perform(curl);
	if (res != CURLE_OK) {
		fprintf(stderr, "curl_easy_perform() failed: %s\n", curl_easy_strerror(res));
	}
	/* Clean up after yourself */
	curl_easy_cleanup(curl);
	return 0;
}
/* See: http://stackoverflow.com/a/2329792/1127848 of how to read data from the response. */
```
