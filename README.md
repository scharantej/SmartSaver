## Flask Application Design for Problem: Build a Browser Extension Surfacing Discount Codes and Coupons for Signed-in Google Users. The Code Appears Based on the Merchant Site the User Is Browsing and the Extension Is Context Aware to Surface the Right Coupon Based on the Product on the Page.

### HTML Files:

- **popup.html**: This file will serve as the extension's popup user interface. It will display the list of available coupons and discount codes for the current website.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Coupons</title>
  </head>
  <body>
    <h1>Available Coupons</h1>
    <ul id="coupons">
    </ul>
  </body>
</html>
```

### Routes:

- **get_coupons()**: This route will handle the request for coupons based on the current website. It will retrieve the available coupons and discount codes from the server and return them as a JSON response.

```python
@bp.route('/get_coupons', methods=['GET'])
def get_coupons():
    """Get coupons for the current website."""
    merchant_id = get_merchant_id()
    coupons = store.get_coupons_for_merchant(merchant_id)
    return jsonify(coupons)
```

- **apply_coupon()**: This route will handle the application of a coupon to the current purchase. It will send the coupon code to the merchant's website and attempt to apply the discount.

```python
@bp.route('/apply_coupon', methods=['POST'])
def apply_coupon():
    """Apply a coupon to the current purchase."""
    coupon_code = request.form['coupon_code']
    success = apply_coupon_to_purchase(coupon_code)
    return jsonify({'success': success})
```