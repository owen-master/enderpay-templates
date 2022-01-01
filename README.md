# 📄 Enderpay store templates

Enderpay uses the popular Twig templating engine to allow you to customize the look and feel of your webstore.

## Available template variables

### ➡️ Global variables (available on all pages)
The following twig template variables are available on all webstore pages.

**Store:**
```
store.id                // The store ID [int]
store.name              // The store name [string]
store.isBrandingEnabled // If store branding is enabled [bool]
store.alerts            // The stores alerts [array]
store.categories        // The stores categories [array]
store.modules           // The stores modules [array]
store.pages             // The stores pages [array]
store.currencies        // The stores currencies [array]
store.currency          // The stores base currency [array]
store.jsUrl             // Enderpay javascript url [string]
store.themeUrl          // The stores theme url [string]
store.logoUrl           // The stores logo image url [string/null]
store.backgroundUrl     // The stores background image url [string/null]
store.faviconUrl        // The stores favicon image url [string/null]
store.notifications     // The stores notifications [array]
store.csrfToken         // The CSRF token to use on forms [string]
```

**Alerts:**
```
{% for alert in store.alerts %} // Twig loop

    alert.name    // The alert name [string]
    alert.type    // The alert type [string]
    alert.content // The alert content [string]

{% endfor %}
```

**Categories:**
```
{% for category in store.categories %} // Twig loop

    category.name     // The category name [string]
    category.slug     // The category slug [string]
    category.link     // The category link [string]
    category.children // The categories child categories [array]

    {% for child in category.children %} // Twig loop

        category.name     // The category name [string]
        category.slug     // The category slug [string]
        category.link     // The category link [string]

    {% endfor %}

{% endfor %}
```

**Modules:**
```
{% for module in store.modules %} // Twig loop

    module.name // The module name [string]
    module.type // The module type [string]
    module.data // The module data [array]

{% endfor %}
```

**Pages:**
```
{% for page in store.pages %} // Twig loop

    page.name // The page name [string]
    page.slug // The page slug [string]
    page.link // The page link [string]

{% endfor %}
```

**Currencies:**
```
{% for currency in store.currencies %} // Twig loop

    currency.iso4217  // The currency iso4217 [string]
    currency.currency // The currency name [string]
    currency.symbol   // The currency symbol e.g. $ [string]

{% endfor %}
```

**Store base currency:**
```
store.currency.iso4217  // The currency iso4217 [string]
store.currency.currency // The currency name [string]
store.currency.symbol   // The currency symbol e.g. $ [string]
```

**Notifications**
```
{% for notification in store.notifications %} // Twig loop

    notification.type    // The notification type [string]
    notification.message // The notifications message [string]

{% endfor %}
```

**Cart:**
```
cart.storeId       // The store ID [int]
cart.customer      // The customer [array]
cart.packages      // The carts packages [array]
cart.giftcards     // The carts giftcards [array]
cart.currency      // The carts currency [array]
cart.grandTotal    // The cart grand total [float]
```

**Cart packages:**
```
{% for package in cart.packages %} // Twig loop

        package.id            // The package ID [int]
        package.name          // The package name [string]
        package.content       // The package content [string]
        package.isPurchasable // If the package is purchasable [null]
        package.originalPrice // The packages original price [float]
        package.price         // The package price [float]
        package.inCart        // If the package is in the cart [bool]
        package.imageUrl      // The package image [string/null]
        package.quantity      // The package quantity in the cart [int]
        package.variableCount // The package variable count in the cart [int]
        package.createdAt     // When the package was created [string]
        package.updatedAt     // When the package was last updated [string]

{% endfor %}
```

### ➡️ Home page variables (available on the home page)
The following twig template variables are available on the home page.

```
page.title   // The page title [string]
page.content // The page content [string]
```

### ➡️ Category page variables (available on category pages)
The following twig template variables are available on the category page.

**Category information:**
```
category.id        // The category ID [int]
category.name      // The category name [string]
category.slug      // The category slug [string]
category.orderBy   // The category package ordering method [string]
category.viewMode  // The category view mode [string]
category.content   // The category content [string]
category.updatedAt // When the category was last updated [string]
category.packages  // The categories packages [array]
```

**Category packages:**
```
packages = [
    [
        id => 1, // the package ID
        name => 'The package name',
        content => 'The package content',
        isPurchasable => false, // whether or not the package is purchasable (bool/null)
        originalPrice => 5.00, // price with no discounts applied
        price => 0.00, // price with discounts applied (float)
        inCart => true, // if the package is in the cart (bool)
        imageUrl => null, // the image URL of the package (string/null)
        createdAt => '5 minutes ago', // when the package was created
        updatedAt => '1 minute ago', // when the package was last updated
    ],...
]
```

### ➡️ Package page variables (available on package pages)
The following twig template variables are available on the package page. The package page only appears when a package has variables in which customers must provide a value

```
package.id            // The package ID [int]
package.name          // The package name [string]
package.content       // The package content [string]
package.isPurchasable // If the package is purchasable [bool]
package.originalPrice // The packages original price [float]
package.price         // The package price [float]
package.inCart        // If the package is in the cart [bool]
package.imageUrl      // The package image [string/null]
package.variables     // The package variables to be completed by customer [array]
package.createdAt     // When the package was created [string]
package.updatedAt     // When the package was last updated [string]
```

### ➡️ Custom page variables (available on custom pages)
The following twig template variables are available on custom pages.

```
page.name      // The page name [string]
page.content   // The page content [string]
page.createdAt // When the page was created [string]
page.updatedAt // When the page was last updated [string]
```

### ➡️ Checkout page variables (available on the checkout page)
The following twig template variables are available on the checkout page.
```
checkout.gateways // Available payment gateways to use during checkout [array]
checkout.countries // Available countries to use during checkout [array]
```

**Gateways:**
```
{% for gateway in checkout.gateways %} // Twig loop

    gateway.name // The gateway name [string]
    gateway.type // The gateway type [string]

{% endfor %}
```

**Countries:**
```
{% for country in checkout.countries %} // Twig loop

    country.id     // The country ID [int]
    country.name   // The country name [string]
    country.alpha2 // The country ISO 3166-1 alpha-2 [string]
    country.alpha3 // The country ISO 3166-1 alpha-3 [string]

{% endfor %}
```

### ➡️ Checkout success variables (available on the checkout success page)
The following twig template variables are available on the checkout success page.
```
page.title   // The page title [string]
page.content // The page content [string]
```

### ➡️ Module-specific variables

**Custom text module:**
```
data.content // The content [string]
```

**Featured package module:**
```
data.package.id            // The package ID [int]
data.package.name          // The package name [string]
data.package.content       // The package content [string]
data.package.isPurchasable // If the package is purchasable [bool]
data.package.originalPrice // The packages original price [float]
data.package.price         // The package price [float]
data.package.inCart        // If the package is in the cart [bool]
data.package.imageUrl      // The package image [string/null]
data.package.createdAt     // When the package was created [string]
data.package.updatedAt     // When the package was last updated [string]
```

**Featured player module:**
```
data.username // The featured players username [string]
```

**YouTube video module:**
```
data.videoId // The YouTube videos video ID [string]
```

**Recent logins module:**
```
{% for login in data.logins %} // Twig loop

    login.uuid     // The uuid of the player that logged in [string]
    login.username // The username of the player that logged in [string]
    login.when     // When the player logged in [string]

{% endfor %}
```

**Online players module:**
```
{% for player in data.players %} // Twig loop

    payment.uuid       // The players uuid [string]
    payment.username   // The players username [string]

{% endfor %}
```

**Donation goal module:**
```
data.goal       // The donation goal [float]
data.revenue    // The total amount achieved [float]
data.percentage // The percentage completed [float]
data.animated   // If the progress bar should be animated [bool]
```

**Top donator module:**
```
data.username // The username of the top donator [string]
data.uuid     // The uuid of the top donator [string]
data.total    // The total amount of the top donator [float]
```

**Server address module:**
```
data.serverAddress    // The servers address [string]
data.serverPort       // The servers port [string]
data.displayIfOffline // If the module should be displayed if the server is offline [bool]
```

**Recent payments module:**
```
{% for payment in data.recentPayments %} // Twig loop

    payment.uuid       // The payment customers uuid [string]
    payment.username   // The payment customers username [string]
    payment.packages   // The payments packages [array]
    payment.grandTotal // The payments grand total [float]
    payment.when       // When the payment was created [string]

    {% for package in payment.packages %} // Twig loop

        package.name     // The name of the package [string]
        package.quantity // The quantity of the package [int]

    {% endfor %}

{% endfor %}
```
