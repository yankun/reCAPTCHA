## reCAPTCHA Addon for [CouchCMS](http://www.couchcms.com/)
Utilize Google's [reCAPTCHA](https://www.google.com/recaptcha) service in your forms.

### Installation
1. Copy the `recaptcha` folder to the `addons` folder of your Couch installation
2. Visit [https://www.google.com/recaptcha/admin](https://www.google.com/recaptcha/admin) and register your site with Google to enable reCAPTCHA API access
3. Enter the provided API key pair in the `config.php` file found in your `addons/recaptcha` folder
4. Add the following statement to the `kfunctions.php` file found in your `addons` folder (you might have to rename `kfunctions.example.php` to `kfunctions.php` for newer installations)

```PHP
require_once( K_COUCH_DIR.'addons/recaptcha/recaptcha.php' );
```

### Usage

```PHP
<cms:input name='recaptcha_test' type='recaptcha'/>
```

#### Parameters
- `theme`
 - `light` (default)
 - `dark`
- `size`
 - `normal` (default)
 - `compact`

### Notes
You may wish to buffer the output of the reCAPTCHA field, so that it may be hidden upon successful form submission.

```PHP
<cms:capture 'recaptcha_buffer'>
    <cms:input name='recaptcha_test' type='recaptcha' theme='dark' size='compact'/>
</cms:capture>

<cms:if "<cms:not k_success/>">
    <cms:show recaptcha_buffer/>
</cms:if>
```

If you are utilizing this field in a form which may be submitted more than once, without reloading the page (e.g. AJAX), you will need to ask the end user to verify with reCAPTCHA again. This can be accomplished by executing the following JavaScript statement, whereby `n` is the relevant widget ID. Unless you have more than one reCAPTCHA field, this value will be `0`.

```JavaScript
grecaptcha.reset(n);
```
