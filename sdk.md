---
# Page settings
logo: logo.png
layout: section
title: KeyConnect SDK
description: KeyConnect SDK provides integration with KeyConnect API Server, a single gateway to access BTC, ETH and XRP blockchains.
keywords: sdk blockchain eth api xrpl bitcoin btc ether
ogTitle: KeyConnect - SDK
ogDescription: KeyConnect SDK provides integration with KeyConnect API Server, a single gateway to access BTC, ETH and XRP blockchains.
ogImage: og_sdk.png
ogUrl: /sdk

button: 
    label: Get Started
    url: https://www.keyconnect.app/api-docs/index.html
    external_url: true
    style: bordered
    icon: play-circle

section:
    html: 
        <div style="width:80%;margin:0 auto">
        <pre class="prettyprint" style="background:#282840;border-radius:10px"><code class="language-java">
        DefaultApi apiInstance = new DefaultApi(
        <br>
        <span class="u-pl-3">new ApiClient().setBasePath("https://www.keyconnect.app")</span>
        <br>
        );
        <br><br>
        try {
        <br>
        <span class="u-pl-3">ServerStatusResponse result = apiInstance.getServerStatus();
        <br>
        <span class="u-pl-3">System.out.println(result);</span>
        <br>
        } catch (ApiException e) {
        <br>
        <span class="u-pl-3">System.err.println("Exception when calling DefaultApi#getServerStatus");</span>
        <br>
        <span class="u-pl-3">e.printStackTrace();</span>
        <br>
        }
        </pre></code>
        </div>

---
