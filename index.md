---
layout: default
title: PayPal Payment Request Form
description: Simple pay via paypal form
---

***This is a live form to see what happens when you click the link - do not actually complete the form on PayPal!!***

<p>Please pay the amount of your invoice by filling in the fields below (they may be filled in already depending on how you got here) and then clicking the "Pay Now" button.</p>
<p style="padding-bottom:10px;"> If you don't have an order number, you can use your full name as a reference instead.</p>

<form action="https://www.paypal.com/cgi-bin/webscr" method="post">
    <fieldset>
      <input type="hidden" name="business" value="orders@prolabprints.com" />
        <input type="hidden" name="return" value="http://prolabprints.com/paypal-payment-received/" />
        <input type="hidden" name="cancel_return" value="http://prolabprints.com" />
        <input type="hidden" name="cmd" value="_xclick" />
        <input type="hidden" name="lc" value="US" />
        <input type="hidden" name="item_name" value="Payment" />
        <input type="hidden" name="currency_code" value="USD" />
        <input type="hidden" name="button_subtype" value="services" />
        <input type="hidden" name="no_note" value="0" />
        <input type="hidden" name="cn" value="Comments" />
        <input type="hidden" name="no_shipping" value="1" />
        <input type="hidden" name="rm" value="1" />   
        <input type="hidden" name="bn" value="PP-BuyNowBF:btn_paynowCC_LG.gif:NonHostedGuest" />
        <table >
            <tr>
                <td style="padding:0 5px 5px 0;">Amount: </td>
                <td style="padding:0 5px 5px 0;"><input class="form-control" id="amount" type="text" name="amount" maxlength="200" /></td>
            </tr>
            <tr>
                <td style="padding:0 5px 5px 0;">Order #: </td>
                <td style="padding:0 5px 5px 0;"><input class="form-control" id="orderid" type="text" name="os0" maxlength="200" /><input type="hidden" name="on0" value="Order #" /></td></tr>
                <tr>
                    <td>&nbsp;</td><td style="padding:10px 5px 5px 0;">
                    <input class="btn btn-success" type="submit"  name="submit" value="Pay Now via PayPal" alt="PayPal. The safer, easier way to pay online." />
                  <p><img src="https://www.paypalobjects.com/webstatic/en_US/i/buttons/cc-badges-ppmcvdam.png" alt="Buy now with PayPal" /></p>
                    </td>
                </tr>
        </table>
    </fieldset>
</form>

<p style="padding-top:10px;"> <b>This charge will appear on your credit card statement as payment to PAYPAL *PROLABPRINTS.</b></p>
<p>PayPal will give us all of your contact info that you fill in on their payment form, which we will also use to match up your order with this payment.</p>
<p>PayPal accepts all major credit cards, including American Express.</p>
<p>Questions? Give us a call - (111) 111-1111.</p>

<script>function getUrlParams() {

  var paramMap = {};
  if (location.search.length == 0) {
    return paramMap;
}
var parts = location.search.substring(1).split("&");

for (var i = 0; i < parts.length; i ++) {
    var component = parts[i].split("=");
    paramMap [decodeURIComponent(component[0])] = decodeURIComponent(component[1]);
}
return paramMap;
}</script>
<script>var params = getUrlParams();
    if (params.amount) 
    {
        document.getElementById('amount').value = params.amount;
    }
    if (params.orderid) 
    {
        document.getElementById('orderid').value = params.orderid;
    }
</script>

----

----

----

----


# How it Works

All you need to allow people to pay is a form with a bunch of hidden fields that tells PayPal what you do. You don't need any server code, the form works from
just a simple static html page.

If you want to send people a link to pay you can also add in query parameters to give the Order Number and the amount in the URL and then some simple JavaScript can read that in and populate the form.

## The Form

Please note the top 3 lines of inputs require editing to enter in your info - `business` is your PayPal email address, `return` is the page you want them to be returned to after they pay, and `cancel_return` is where they should be sent if they get to PayPal but click cancel. 

The rest of the form should be ok as is.

```
<form action="https://www.paypal.com/cgi-bin/webscr" method="post">
    <fieldset>
        <input type="hidden" name="business" value="orders@prolabprints.com" />
        <input type="hidden" name="return" value="http://prolabprints.com/paypal-payment-received/" />
        <input type="hidden" name="cancel_return" value="http://prolabprints.com" />
        <input type="hidden" name="cmd" value="_xclick" />
        <input type="hidden" name="lc" value="US" />
        <input type="hidden" name="item_name" value="Payment" />
        <input type="hidden" name="currency_code" value="USD" />
        <input type="hidden" name="button_subtype" value="services" />
        <input type="hidden" name="no_note" value="0" />
        <input type="hidden" name="cn" value="Comments" />
        <input type="hidden" name="no_shipping" value="1" />
        <input type="hidden" name="rm" value="1" />   
        <input type="hidden" name="bn" value="PP-BuyNowBF:btn_paynowCC_LG.gif:NonHostedGuest" />
        <table >
            <tr>
                <td style="padding:0 5px 5px 0;">Amount: </td>
                <td style="padding:0 5px 5px 0;"><input class="form-control" id="amount" type="text" name="amount" maxlength="200" /></td>
            </tr>
            <tr>
                <td style="padding:0 5px 5px 0;">Order #: </td>
                <td style="padding:0 5px 5px 0;"><input class="form-control" id="orderid" type="text" name="os0" maxlength="200" /><input type="hidden" name="on0" value="Order #" /></td></tr>
                <tr>
                    <td>&nbsp;</td><td style="padding:10px 5px 5px 0;">
                    <input class="btn btn-success" type="submit"  name="submit" value="Pay Now via PayPal" alt="PayPal. The safer, easier way to pay online." />
                  <p><img src="https://www.paypalobjects.com/webstatic/en_US/i/buttons/cc-badges-ppmcvdam.png" alt="Buy now with PayPal" /></p>
                </td>
            </tr>
        </table>
    </fieldset>
</form>

```

## JavaScript to Populate the Order Number and Amount Fields

This is fairly simple, but makes it so you can send a properly formatted link that when clicked will take them to the form and the amount and order number will already be filled in.

This is done with query string parameters. Query strings appear at the end of a url and begin with a ? and are followed by named value pairs. They can be strung together with an ampersand (&).

For example, if the amount is $125.50 and the order number is 188212, the url could be like:

**mysite.com/payment/?orderid=188212&amount=125.50**

You can put this code at the bottom of the html page.

```
<script>function getUrlParams() {

  var paramMap = {};
  if (location.search.length == 0) {
    return paramMap;
}
var parts = location.search.substring(1).split("&");

for (var i = 0; i < parts.length; i ++) {
    var component = parts[i].split("=");
    paramMap [decodeURIComponent(component[0])] = decodeURIComponent(component[1]);
}
return paramMap;
}</script>
<script>var params = getUrlParams();
    if (params.amount) 
    {
        document.getElementById('amount').value = params.amount;
    }
    if (params.orderid) 
    {
        document.getElementById('orderid').value = params.orderid;
    }
</script>
```