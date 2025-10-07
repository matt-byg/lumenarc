# Cart Persistence Enhancement - Installation Guide

This package provides cart quantity persistence functionality for Shopify themes, allowing cart changes to be saved when users navigate away from the cart page.

## 🎯 What This Provides

- ✅ **Cart quantity changes persist** when navigating away from cart page
- ✅ **Real-time header cart count updates** 
- ✅ **Works with both direct input changes and plus/minus buttons**
- ✅ **Comprehensive debugging** for troubleshooting
- ✅ **AI header cart count updates** (if using AI-generated headers)
- ✅ **Improved cart styling** with proper spacing and image sizing

## 📦 Installation Steps

### Step 1: Add the Snippet
1. Copy `snippets/cart-persistence-enhancement.liquid` to your theme's `snippets` folder
2. In your theme's `layout/theme.liquid` file, add this line before the closing `</body>` tag:

```liquid
{% render 'cart-persistence-enhancement' %}
```

### Step 2: Update Cart Template (if using contact form)
If your cart page uses a contact form instead of a cart form, ensure your quantity inputs have the `data-line-id` attribute:

```liquid
<input
  class="quantity"
  type="number"
  name="contact[Product-{{ totalQty }}-Quantity]"
  value="{{ item.quantity }}"
  data-line-id="{{ forloop.index }}"
>
```

### Step 3: Test the Installation
1. Go to your cart page
2. Open browser console (F12)
3. Change a quantity
4. You should see debug messages like:
   ```
   🛒 CART PAGE DETECTED - Setting up handlers
   === CHANGE EVENT DEBUG ===
   ✅ CART UPDATE SUCCESS:
   ```

## 🔧 Customization Options

### Cart Count Selectors
The script automatically updates these cart count elements:
- `.cart_count`
- `.quote-cart-count-top`
- `.quote-cart-count`
- `.cart-count-number`
- `[class*="ai-top-header-bar-cart-count"]`

To add more selectors, edit the `refreshCart` function in the snippet.

### Debug Mode
To disable debug logging, remove or comment out the `console.log` statements in the snippet.

## 🐛 Troubleshooting

### Cart Changes Not Persisting
1. Check browser console for error messages
2. Verify quantity inputs have `data-line-id` attributes
3. Ensure the snippet is loaded (check for "Cart Persistence Enhancement loaded" message)

### Header Not Updating
1. Check if your header cart count elements match the selectors in the script
2. Add custom selectors to the `refreshCart` function if needed

### Plus/Minus Buttons Not Working
1. Ensure buttons have the `js-change-quantity` class
2. Check that the parent container has the correct class (`.purchase-details__quantity` or `.cart--info-wrapper`)

## 📋 Requirements

- Shopify theme with cart functionality
- Quantity inputs with `data-line-id` attributes
- Modern browser with fetch API support

## 🚀 Advanced Usage

### Custom Cart Count Selectors
Add your own selectors to the `refreshCart` function:

```javascript
// Add your custom selector
document.querySelectorAll('.your-custom-cart-count').forEach(function(node){
  node.textContent = cart.item_count;
});
```

### Custom Event Handling
The script uses event delegation, so it will work with dynamically added cart items.

## 📞 Support

If you encounter issues:
1. Check the browser console for error messages
2. Verify all installation steps were completed
3. Test with a simple cart setup first

## 🔄 Updates

To update the enhancement:
1. Replace the snippet file with the new version
2. Clear any cached files
3. Test the functionality

---

**Note:** This enhancement works with most Shopify themes but may require minor adjustments for custom cart implementations.
