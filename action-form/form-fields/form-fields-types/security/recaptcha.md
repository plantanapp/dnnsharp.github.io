# reCAPTCHA 

In order to detect abusive traffic on your website and prevent spam form submissions from being executed by bots you should use Google reCAPTCHA.

The reCAPTCHA field can be easily added on your online form by selecting it from *Add Field &gt; Security &gt; reCAPTCHA*. 

By default, the field is set to be always visible on page as seen in the image below
![Google reCAPTCHA](https://static.dnnsharp.com/documentation/google_recaptcha_form_field.png 'Google reCAPTCHA')
but it can also be set as **Invisible**. Take note that *API key* and *secret key* are different for regular and invisible reCAPTCHA.

> Invisible reCAPTCHA was added in [Action Form 5.0.501](https://www.dnnsharp.com/download?p=AFORM&v=05.00.501) 

>Starting with [Action Form 5.0.573](https://www.dnnsharp.com/download?p=AFORM&v=05.00.573) the reCAPTCHA field token *[field_name]* stores true/false as value and therefore can be used in **bind expression** to condition visibility for other form fields.