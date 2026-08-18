# Code

Created by: MD Rakibul Islam Shanto
Created time: December 10, 2024 2:32 PM
Tags: Custom Code

### Template Generator Code

[https://muhtasimmahir.github.io/ZeptoAppsTemplateGenerator/](https://muhtasimmahir.github.io/ZeptoAppsTemplateGenerator/)

### Restrict Upload file format (ex. only .png format is acceptable)

```jsx
$(".pplr-wrapper input.fileupload[name]").each(function () {
    $(this).attr("accept", "image/png")
   $(this).removeAttr("onchange")
    $(this).off("change").on("change", function (event) {
        const file = this.files[0]
        console.log(file, this.files, this)
        if (file?.name?.split(".")[1] == 'png') {
          fileuploadpplr(this,event)
        } else {
            alert("only png image type is allowed")
            this.value = null
            this.files = null
            return
        }
    })
})
```

### Restrict the upload file format (one or multiple) 

```jsx
$(".pplr-wrapper input.fileupload[name]").each(function () {
    $(this).attr("accept", "image/png")
    $(this).removeAttr("onchange")
    $(this).off("change").on("change", function (event) {
        const file = this.files[0]
        const ext = file?.name?.split(".").pop()?.toLowerCase()

        if (ext === "webp" || ext === "gif" || ext === "jpg" || ext === "jpeg" || ext === "bmp" || ext === "svg") {
            alert("This format is not allowed")
            this.value = null
            return
        }

        fileuploadpplr(this, event)
    })
})
```

### How to make text field color required?

```jsx
$('.pplr-swatch-element.pplrColor.color_image_display_box').addClass('cstmfy_c_required').attr('required', true);
```

### How to stop all create new product from theme.liquid

```jsx
$('.pplr-swatch-element.pplrColor.color_image_display_box').addClass('cstmfy_c_required').attr('required', true);
```

### How to prevent Auto Tab Switch

```jsx
window.PPLR_PREVENT_AUTO_TAB = true;
```

### Changing position of App Block with JS

```jsx
$('.product-personalizer').after($('.product-form__option-selector'));
```

### How to disable a field (Image Choice) from clicking using jQuery

```jsx
$(document).ready(function () {
    // Select all elements with name="properties[INCLUSIVE]"
    $('[name="properties[INCLUSIVE]"]').each(function () {
        // Remove the onclick attribute
        $(this).removeAttr('onclick');
        // Disable pointer events to make it non-clickable
        $(this).css('pointer-events', 'none');
        // Optional: Add a class to visually indicate it's disabled (if needed)
        $(this).addClass('disabled');
    });
});

```

### CSS class for Developer Settings

```jsx
tr:has(.cart-item__quantity) -> row class

dl .product-option:not(:first-of-type) -> wrapper class
```

### Product unavailability after creating new product issue

```jsx
window.pplr_atc_delay = 1000;
```

1000 means 1 second; you can add more times if issue persist. If not solved then you can contact us. 

### Making the default quantity 1 in popup

```jsx
$(document).on("click", ".add-monogram-btn", function () {
    $('.q_fi[name="quantity"]').val(1);
});
```

### Dividing price by 4 (Custom work - #65572)

```jsx
$(document).ready(function () {
    let prevPrice = $('.price-list').text().trim(); // Store initial price
    let timeout = null; // Store timeout reference

    let observer = new MutationObserver(function () {
        let newPrice = $('.price-list').text().trim();

        if (newPrice !== prevPrice) { // Only update if price changes
            prevPrice = newPrice; // Update stored price

            // Clear any previous timeout to prevent instant change
            clearTimeout(timeout);

            timeout = setTimeout(function () {
                let price = parseFloat(newPrice.replace(/[^0-9.]/g, ''));
                if (!isNaN(price)) {
                    $('.4fois').text((price / 4).toFixed(2));
                }
            }, 2000); // 2-second delay
        }
    });

    observer.observe(document.querySelector('.price-list'), {
        childList: true,
        subtree: true,
        characterData: true
    });
});
```

The total price gets divided by 4 after every time change of price. It will work after 2 seconds delay. 

![image.png](Code/image.png)

### Trigger code for custom button ‘Personalize it’ (Custom - #65576)

```jsx
$(document).ready(function() {
     $('.zeptoCustomButton').on('click', function(event) {
         cstmfy_personalize_text(this, event);
     });
});
```

![image.png](Code/image%201.png)

### JS for filtering words in text field (custom - #65565)

OLD 

```jsx
document.addEventListener("DOMContentLoaded", function () {
  // Select the textarea element
  const textarea = document.querySelector('textarea[name="properties[Single Line Text]"]');

  if (textarea) {
    // Add an event listener for the 'input' event
    textarea.addEventListener("input", function (event) {
      // Get the current value of the textarea
      let inputText = event.target.value;

      // Define the words to filter (case-insensitive)
      const wordsToFilter = ["india", "abcd", "zepto"];

      // Create a regular expression to match any of the words
      const regex = new RegExp(`\\b(${wordsToFilter.join("|")})\\b`, "gi");

      // Remove the filtered words
      inputText = inputText.replace(regex, "");

      // Update the textarea value with the filtered text
      event.target.value = inputText;
    });
  } else {
    console.error("Textarea not found!");
  }
});
```

```jsx
<script src="{{ 'customwork.js' | asset_url }}" defer="defer" type="text/javascript"></script>
```

New

```jsx

function initWordFilter() {
  const input = document.querySelector('input[name="properties[Enter your name]"]');

  if (input) {
    input.removeAttribute("oninput");

    input.addEventListener("input", function (event) {
      let inputText = event.target.value;

      const wordsToFilter = ["xyz", "abcd", "zepto"];
      const regex = new RegExp(`\\b(${wordsToFilter.join("|")})\\b`, "gi");
      inputText = inputText.replace(regex, "");

      event.target.value = inputText;

      LoadPplrWithFont('2', true, event.target);
    });

    console.log("PPLR word filter initialized.");
  }
}

// Watch the DOM until the input appears
const observer = new MutationObserver(function (mutations, obs) {
  const input = document.querySelector('input[name="properties[Enter your name]"]');
  if (input) {
    initWordFilter();
    obs.disconnect(); // Stop observing once found
  }
});

observer.observe(document.body, {
  childList: true,
  subtree: true
});

```
### Showing product image in cart page

```html
<img class="pplr_original_img">
```

### COGS / loader icon change with CSS

```css
.pplr_loader {
   background: url('https://cdn.shopify.com/s/files/1/0670/1734/3033/files/Gif-Aurora.gif?v=1729181642') !important;
   background-repeat: no-repeat !important;
   background-position: center !important;
}
```

```css
.pplr_loader {
   visibility: none !important;
}
```

### Blocking ‘space’ button from the input field (custom - #66551)

```jsx
$(document).ready(function () {
    $(document).on('keydown', '.pplr_text.pplr_monogram', function (event) {
        if (event.key === ' ' || event.keyCode === 32) {
            event.preventDefault();
        }
    });
});
```

### Showing 1 quantity price even after updating the quantity in product page

```jsx
window.pplr_no_qty_update = true;
```

### Disabling viewport/ pplr_meta to enable the zooming in mobile

```jsx
window.pplr_no_meta = true;
```

### Checkbox CSS

```css
input[type="checkbox"].pplrcheckbox {
  appearance: auto !important;
  -webkit-appearance: checkbox !important;
  -moz-appearance: checkbox !important;
  width: 16px !important;
  height: 16px !important;
  display: inline-block !important;
  visibility: visible !important;
  opacity: 1 !important;
  position: static !important;
  clip: auto !important;
  margin: 5px;
}
```

```css
.pplr-wrapper label {
    width: auto !important;
    float: left !important;
    margin-right: 8px !important;
    padding: 10px 0px !important;
}

input[type=checkbox] {
    display: inline-block !important;
    width: auto !important;
    margin: 0px 3px !important;
}
```

### Making Radio button from Checkbox using CSS

```css
input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  width: 16px;
  height: 16px;
  border: 2px solid #555;
  border-radius: 50%;
  position: relative;
  cursor: pointer;
  vertical-align: middle;
  margin-right: 8px;
}

input[type="checkbox"]:checked::before {
  content: "";
  position: absolute;
  top: 4px;
  left: 4px;
  width: 6px;
  height: 6px;
  background-color: #555;
  border-radius: 50%;
}
```

### JS code for changing popup button name

```jsx
const button = document.querySelector('button.btn.pplr-c-button.pplr-btn.button.Button--secondary.ptc_button');
if (button) {
  button.textContent = "Make It Yours";
}
```

### Extension JS code for copying the myshopify URL

```jsx
// ==UserScript==
// @name         Add Copy Button for myshopify Domain on Zendesk
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Add "Copy myshopify domain" button beside links in Zendesk that contain shop=xxx.myshopify.com
// @author       Rakib
// @match        https://product-personalizer.zendesk.com/*
// @grant        GM_setClipboard
// ==/UserScript==

(function () {
    'use strict';

    const observer = new MutationObserver(() => {
        const links = document.querySelectorAll('a[href*="shop="]');
        links.forEach(link => {
            const href = link.href;
            if (link.nextSibling && link.nextSibling.classList && link.nextSibling.classList.contains('copy-myshopify-btn')) {
                return; // Button already exists
            }

            const match = href.match(/shop=([a-zA-Z0-9\-]+\.myshopify\.com)/);
            if (match && match[1]) {
                const domain = match[1];
                const btn = document.createElement('button');
                btn.textContent = '📋 Copy shop domain';
                btn.style.marginLeft = '6px';
                btn.style.padding = '2px 6px';
                btn.style.fontSize = '12px';
                btn.style.cursor = 'pointer';
                btn.style.borderRadius = '4px';
                btn.style.border = '1px solid #ccc';
                btn.className = 'copy-myshopify-btn';

                btn.addEventListener('click', function (e) {
                    e.preventDefault();
                    GM_setClipboard(domain);
                    btn.textContent = '✅ Copied!';
                    setTimeout(() => (btn.textContent = '📋 Copy shop domain'), 2000);
                });

                link.parentNode.insertBefore(btn, link.nextSibling);
            }
        });
    });

    observer.observe(document.body, { childList: true, subtree: true });
})();

```

### Calendar / Changing format of date to ‘dd/mm/yyyy’

```jsx
jQuery("head").append('<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">')
loadScript_p("https://cdn.jsdelivr.net/npm/flatpickr", () => {
    jQuery('.pplr-wrapper input[type="date"]').attr("placeholder", 'dd.mm.yyyy')
    flatpickr('.pplr-wrapper input[type="date"]', {
        dateFormat: "d.m.Y",
         allowInput: true
     })

Object.keys(pplr_values).map((key) => {
    if(pplr_values[key][38] == 5){
        pplr_values[key][38] = 1
    }
})
})
```

### ‘Out of Stock’ text change + color modify

```css
*, *::before, *::after {
    box-sizing: inherit;
    color: black !important;
}
.vrdisabled::before {
    content: 'Sold Out' !important;
}
```

### How to design the ATC button with an image

```jsx
var tries = 0;
var maxTries = 60;

function checkZeptoButton() {
  var zeptoOriginal = document.querySelector("button.ptc_button");
  if (zeptoOriginal) {
    var container = zeptoOriginal.closest(".product-personalizer");
    if (!container) container = zeptoOriginal.parentNode;
    container.innerHTML = "";

    var wrapper = document.createElement("div");
    wrapper.className = "zepto-wrapper";

    var img = document.createElement("img");
    img.className = "carcasas-trio";
    img.src = "https://cdn.shopify.com/s/files/1/0628/6006/6873/files/billeterasmuestra.png?v=1749052464";
    img.alt = "Tres carcasas Limited – personaliza aquí";
    img.onerror = function() {
      console.warn("Image failed to load, hiding img.");
      img.style.display = "none";
    };

    var customBtn = document.createElement("button");
    customBtn.className = "zepto-custom-btn";
    customBtn.textContent = "Personaliza aquí!";

    wrapper.appendChild(img);
    wrapper.appendChild(customBtn);
    container.appendChild(wrapper);

    zeptoOriginal.style.display = "none";
    container.appendChild(zeptoOriginal);

    customBtn.addEventListener("click", function() {
      zeptoOriginal.click();
    });
  } else {
    tries++;
    if (tries < maxTries) setTimeout(checkZeptoButton, 300);
  }
}

checkZeptoButton();

```

### All Code

```jsx
1. window.pplr_atc_delay = 1000; 
2. window.pplr_svg2pdf = true; 
3. window.pplr_no_qty_update = true; 
4. window.pplr_create_disabled = true; 
5. window.pplr_no_carousel= true;
6. window.pplr_custom_allowed_types = ['mp4a']; // ['jpg','jpeg','png','gif','webp','avif','bmp','svg','svg+xml','heic'] 
6. window.PPLR_PREVENT_AUTO_TAB = true; 
7. window.pplr_currency_adjust = true; 
8. window.pplr_shopify_file_size=7; 
9. window.pplr_slide_animation=false; 
10. window.pplr_s3_upload = true; 
11. pplr_hide_attributes_from_bundle = false; 
12. show_additionl_product = true; 
13. window.pplr_date_format = "dd-mm-yyyy"
14. window.pplr_png_preview = true    // making the preview in PNG format 
15. window.pplr_scroll_lock = () => {};  // scrolling issue in phone 
```

### JS code to force for p_a_t_c class in ATC button

```jsx
$('.product-form,.pplrform').find('[name="add"][type="submit"]').addClass("p_a_t_c")
```

### How to check price from console?

```jsx
document.querySelectorAll('[data-pplr_price]').forEach(el => {
  console.log(el.getAttribute('name'), el.dataset.pplr_price);
});
```

### (Personal) Asset image delete code from console

```jsx
deleteFontImage(window.sets.images.store.splice(0, 100), 'image')
```

### For color required set for text fields.

```jsx
$(".pplrgcolor").siblings("input.cstmfy_c_required").val("").attr("data-value", "").attr("value", "").attr("data-type", "5")
$(".pplrgcolor .selected").removeClass("selected")

var prev_pplr_check_require = pplr_check_require;
window.pplr_check_require = (pplrtis,e,k) => {
    $(".pplrgcolor").siblings("input.cstmfy_c_required").each(function(){
        if($(this).attr('data-type') == 5){
            $(this).attr("data-value", "").val("")
        }
    })
    prev_pplr_check_require(pplrtis,e,k);
}
```

### To change the extra keyboard color & icon

New format
```css
.key_layout_sub {
color: red !important;   /* this for color */
}

.key_layout span {
     border-radius: 60px !important;
}
```
```js
var prev_cstmfy_personalize_text = cstmfy_personalize_text;
 $('.key_layout_sub').text('℞')
window. cstmfy_personalize_text = (a, b) => {
prev_cstmfy_personalize_text(a, b)
   $('.key_layout_sub').text('℞')
}
```

Old format
```css
.key_layout_sub {
color: red !important;   /* this for color */
}

.key_layout_sub {
font-size: 0;      /* for hiding the old emoji */
}

.key_layout_sub::before {
content: "🖮";      /* this for new emoji or icon */
font-size: 4rem;    /* here you can adjust the size of the new icon */
}
```

### Js to capitalize first character of every word

```jsx
$(document).ready(function() {
  $(document).on('input', '.pplr_text', function() {
    $(this).val($(this).val().replace(/\b\w/g, txt => txt.toUpperCase()));
    console.log('Input changed!'); // console check
  });
});
```

```jsx
<script src="{{ 'custom-script.js' | asset_url }}" defer="defer" type="text/javascript"></script>

```

![image.png](Code/image%202.png)

### To block entering emoji in the text field

```jsx
$(document).on('input', '.pplr-wrapper .pplr_text', function () {
        this.value = this.value.replace(
            /([\uD83C-\uDBFF\uDC00-\uDFFF]+)/g,
            ''
        );
    });
```

### Restrict Emojis when Character type is ALL (updated)

```jsx

$(document).on('input', '.pplr-wrapper .pplr_text', function () {
    this.value = this.value.replace(
        /[\u{1F300}-\u{1F6FF}\u{1F900}-\u{1F9FF}\u{1FA00}-\u{1FAFF}\u{2600}-\u{27BF}]/gu,
        ''
    );
});

```

### Packing slip (usually from 132 line)

```jsx
{%- comment -%}ZPPLR_PROPS_BLOCK{%- endcomment -%}

{% for p in line_item.properties %}

  {% unless p.last == blank %}

    {{ p.first }}:

    {% if p.last contains '/uploads/' or p.last contains '/assets/' or p.last contains '/products/' %}
      <img style="width:50px;height:auto" src="{{ p.last }}" />
    {% else %}
      {{ p.last | newline_to_br }}
    {% endif %}

    <br>

  {% endunless %}

{% endfor %}
```

### Mobile sticky preview size CSS

```css
@media (max-width: 768px) {
  .pplr-prev-left {
      width: 60% !important;
  }

  .pplrabs {
      display: flex;
      justify-content: center;
      background: white;
  }
}
```

### To clear the blury color swatch

```css
.pplr-color-select .pplrgcolor .pplr-swatch-element {
    background-position: center center !important;
    background-size: cover !important;
    background-repeat: no-repeat !important;
}
```

### If anyone asks for extra Zoom, we can add this CSS. Nice zoom and smooth effect.

```css
.pplr_preview_wrapper .pplr_zoom,
.pplr-prev-left .pplr_zoom {
    transition: 
        transform 0.3s ease-in-out,
        left 0.15s linear,
        top 0.15s linear;
    will-change: transform, left, top;
}
.pplr_preview_wrapper .pplr_zoom:hover,
.pplr-prev-left .pplr_zoom:hover {
    max-width: none;
    max-height: none !important;
    position: absolute;
    cursor: crosshair;
    transform: scale(1.5);
}
```
---

### When add-to-cart is not handling by our app

```jsx
/**************
 Product ATC
 ***************/

document.querySelector("#productATC").addEventListener("click", async function () {
    // add loading animation
    document.querySelector("#productATC").classList.add("loading");

    let formData = {
        quantity: 1,
        id: activeVariant.id,
    };

    if (personalizeEl && personalizeEl.value.length > 0) {
        formData.properties = {
            Personalize: personalizeEl.value
        };
    }

    // Only this block was added inside the ATC click handler, right before await addProduct(formData): 
    // Collect PPLR app properties
    const pplrProperties = {};
    document.querySelectorAll('.pplr-wrapper input[name], .pplrform input[name]').forEach(function (input) {
        if (input.value) {
            const match = input.name.match(/properties\[(.+)\]/);
            if (match) {
                pplrProperties[match[1]] = input.value;
            } else {
                pplrProperties[input.name] = input.value;
            }
        }
    });

    if (Object.keys(pplrProperties).length > 0) {
        formData.properties = Object.assign({}, formData.properties || {}, pplrProperties);
    }

    // add product
    await addProduct(formData);

    // open cart
    openCart();

    // remove loading animation
    setTimeout(function () {
        document.querySelector("#productATC").classList.remove("loading");
    }, 500);
});
```

---

### JS Code backup
There is a liquid variant limit of 250. The code below works correctly when the variant is higher than 250. 
Product - https://daintygold.co/products/baguette-birthstone-bracelet || thread link - https://discord.com/channels/1298600433866113085/1498324031596793986 || shop: "bpt06w-yh.myshopify.com" 

```jsx
const prev_pplr_variant_title = pplr_variant_title;
window.pplr_variant_title = (v) => {
    const variantFrom = new FormData(jQuery(".variant-picker__form")[0]);
    const variantValues = [];
    for(const variantVal of variantFrom){
        if(variantVal[1]){
            variantValues.push(variantVal[1])
        }
    }
    if(variantValues.length > 0){
        return variantValues.join(" / ");
    }
    return prev_pplr_variant_title(v);
}
updatecondition(1);
```

### For Rebuy Drawer cart
Rebuy drawer cart loads the dom later, for which our common.js file doesn't work on the drawer cart because it loads too fast. The code below can be used before the </head> closing tag, and the common.js script will load later. It will display the personalized image and details in our format. This is for the Rebuy Drawer cart only. [theme_export__evereco-com-au-zepto-copy-of-alinga-2-0-evereco-winback__04JUN2026-0713pm.zip](https://github.com/user-attachments/files/28637023/theme_export__evereco-com-au-zepto-copy-of-alinga-2-0-evereco-winback__04JUN2026-0713pm.zip) 
<br> [Store-link](ever-eco.myshopify.com) 


```jsx
{% comment %} Start {% endcomment %}

<script>
document.addEventListener('DOMContentLoaded', function() {
  var wasVisible = false;
  
  setInterval(function() {
    var rebuyCart = document.querySelector('.rebuy-cart');
    if (!rebuyCart) return;
    
    var isVisible = rebuyCart.classList.contains('is-visible');
    
    if (isVisible && !wasVisible) {
      wasVisible = true;
      setTimeout(function() {
        // Remove old script
        var old = document.getElementById('pplr-common-script');
        if (old) old.remove();

        // Reload pplr_common.js fresh
        var newScript = document.createElement('script');
        newScript.id = 'pplr-common-script';
        newScript.src = 'https://cdn-zeptoapps.com/product-personalizer/pplr_common.js?v=' + new Date().getTime();
        newScript.onload = function() {
          console.log('pplr_common reloaded');
          if (typeof window.pplrReadyInitialization === 'function') {
            window.pplrReadyInitialization();
            console.log('PPLR reinitialized');
          }
        };
        document.head.appendChild(newScript);
      }, 800);
    }
    
    if (!isVisible) {
      wasVisible = false;
    }
  }, 300);
});
</script>

{% comment %} end {% endcomment %}
```

---

### Converting the 'Link-variant' to 'Price Change' 

```jsx
document.querySelectorAll('select[name="price_var[]"]').forEach(function(select){if(select.value==='1'){select.value='0';var container=select.nextElementSibling;if(container){var selectedText=container.querySelector('.custom-select-selected .text');if(selectedText)selectedText.textContent='Price Change';var options=container.querySelectorAll('.custom-select-option');options.forEach(function(opt){if(opt.getAttribute('data-value')==='1')opt.classList.remove('active');if(opt.getAttribute('data-value')==='0')opt.classList.add('active');})}var event=new Event('change',{bubbles:true});select.dispatchEvent(event);}});console.log('Done!');
```

---

### Disable all 'create a new product' methods from all products

```jsx
    window.createproduct = 3;
    _CP[7] = 3;
```

---

### When live preview is not showing after changing the featured image from the thumbnail images (theme side / bottom images) 

```jsx
document.onclick = function (e) {
  var el = e.target;
  var found = 0;
  var p = el;
  for (var i = 0; i < 8; i++) {
    if (!p) break;
    if (p.className && (p.className + '').indexOf('product-personalizer') > -1) {
      found = 1;
    }
    p = p.parentElement;
  }
  if (found === 0) return;

  setTimeout(function () {
    var slides = document.getElementsByClassName('t4s-product__media-item');
    for (var j = 0; j < slides.length; j++) {
      slides[j].className = slides[j].className.replace(' is-selected', '').replace('is-selected', '');
      slides[j].setAttribute('aria-hidden', 'true');
    }
    if (slides[0]) {
      slides[0].className = slides[0].className + ' is-selected';
      slides[0].removeAttribute('aria-hidden');
    }
  }, 100);
};
```

---

### Scrolling issue of the font drop-down (iOS)
Issue video - https://www.loom.com/share/cfa079174d13408a909a5f7133b36914 
```css
@media screen and (max-width: 768px) {
    .pplr-modal-body .pplr-selecter-options {
       position:relative!important;
     }
}
```
---

Another method used for this product - https://hanprinting.com/collections/sticker-font-preview/products/fontpreview 
CSS
```css
@media screen and (max-width: 768px) {
    .pplr-font-select .pplr-selecter-options {
        position: relative !important;
        overflow-y: auto !important;
        -webkit-overflow-scrolling: touch;
        max-height: 250px;
        overscroll-behavior: contain;
    }
}
```
+ JS
```jsx
!function(){var f=function(){document.querySelectorAll('.pplr-selecter-options').forEach(function(d){if(d.dataset.x)return;d.dataset.x=1;var s=0;d.addEventListener('touchstart',function(e){s=e.touches[0].pageY},{passive:!0});d.addEventListener('touchmove',function(e){var y=e.touches[0].pageY,dy=s-y,st=d.scrollTop,sh=d.scrollHeight,ch=d.clientHeight;if(st<=0&&dy<0){e.preventDefault();return}if(st+ch>=sh&&dy>0){e.preventDefault();return}e.stopPropagation()},{passive:!1})})};document.readyState==='loading'?document.addEventListener('DOMContentLoaded',f):f();new MutationObserver(f).observe(document.body,{childList:!0,subtree:!0})}()
```

---

### Changing multiple label names using Custom JS

```jsx
    jQuery(document).ready(function($) {
    var charmNames = {
        'one':   '1st Charms',
        'two':   '2nd Charms',
        'three': '3rd Charms',
        'four':  '4th Charms',
        'five':  '5th Charms',
        'six':   '6th Charms',
        'seven': '7th Charms'
    };

    function renameConditionalLabels() {
        $.each(charmNames, function(numberWord, newName) {
            var $label = $('.pplr-charms-' + numberWord + ' label.pplrlabel');
            
            if ($label.length && $label.text().indexOf(newName) === -1) {
                $label.html(newName + ' <span class="pplr_option_price_span"></span>');
            }
        });
    }
    renameConditionalLabels();
    setInterval(renameConditionalLabels, 300);
    });

```


---

### To stop the click event of the theme using CSS

```css
    .product__media-toggle.product__media-zoom-lightbox {
       pointer-events: none !important;
       cursor: default !important;
    }
```

---

### If the `pplr-character-count` span is missing totally in Text Area

```jsx

    function addCharacterCounters() {
      var wrappers = document.querySelectorAll('.pplr-wrapper.pplr-text');
      for (var i = 0; i < wrappers.length; i++) {
        var wrapper = wrappers[i];
        var ta = wrapper.querySelector('textarea');
        if (!ta) continue;
        if (wrapper.querySelector('.pplr-character-count')) continue;
        wrapper.classList.add('p_c_c');
        var max = ta.getAttribute('data-maxlength') || '0';
        var frame = ta.getAttribute('data-frame') || ta.getAttribute('data-main') || '0';
        var span = document.createElement('span');
        span.className = 'pplr-character-count';
        span.setAttribute('data-frame', frame);
        span.innerHTML = '<span class="ct">' + max + '</span> <span class="lt">characters left</span><span class="lm"> / ' + max + '</span>';
        ta.parentNode.insertBefore(span, ta.nextSibling);
      }
    }
    
    // Run once on load
    addCharacterCounters();
    
    // Watch for PPLR re-rendering on variant change
    var observer = new MutationObserver(function(mutations) {
      for (var i = 0; i < mutations.length; i++) {
        if (mutations[i].addedNodes.length > 0) {
          addCharacterCounters();
          break;
        }
      }
    });
    
    observer.observe(document.body, {
      childList: true,
      subtree: true
    });

```

---

### When the text field cannot be selected or used to add any text on iPhone devices only

Product link -  https://dfu2vzjso2qo89wc-75574706334.shopifypreview.com/products/personalized-premium-wooden-bear-puzzle-premium-wooden-family-bear-christmas-family-keepsake 

```jsx

document.querySelector('.product-personalizer').addEventListener('touchend', e => {
    e.stopImmediatePropagation();
}, true);

```

---

### For taking the product listing from the 'Product Options' of CDN

Run this code in the browser console on the PPLR app products page. Run it once per page — it accumulates names across pages and opens a popup with the full numbered list each time.

Example Steps:
1. Go to page 1 → run the code → popup shows names 1-50
2. Go to page 2 → run the same code again → popup shows names 1-100
3. Go to page 3 → run the same code again → popup shows names 1-150 ✅
4. Copy all from the last popup → paste into Excel/Sheets/Notepad

Notes:
- Duplicate names are automatically skipped
- Always use the last popup — it has the complete list
- If you refresh the page, `window.pplrProductNames` resets — start from page 1 again
- Works on any page size (50, 100, etc.)

The code:
```jsx
if (!window.pplrProductNames) window.pplrProductNames = [];
document.querySelectorAll('tr.hover_row td.title .name span').forEach(function(el) {
  var name = el.textContent.trim();
  if (name && window.pplrProductNames.indexOf(name) === -1) {
    window.pplrProductNames.push(name);
  }
});
var text = window.pplrProductNames.map(function(n, i) { return (i+1) + '. ' + n; }).join('\n');
var win = window.open('', '_blank', 'width=600,height=400');
win.document.write('<pre style="font-family:Arial;font-size:13px;padding:20px;">' + text + '</pre>');
win.document.close();
console.log('Total collected so far:', window.pplrProductNames.length);
```

---

### Adding a smooth transition to the sticky preview image
Only for mobile devices

CSS 
```css
@media screen and (max-width: 768px) {
    .pplrabs {
        /* Force the browser to treat this as a smooth animation layer */
        transition: transform 0.4s ease-in-out !important;
        transform: translateZ(0) !important;
        backface-visibility: hidden !important;
        
        /* Sometimes adding a tiny delay helps the browser catch up */
        animation: smoothFade 0.5s ease-in-out;
    }

    @keyframes smoothFade {
        0% { opacity: 0.8; transform: scale(0.99); }
        100% { opacity: 1; transform: scale(1); }
    }
    
    /* Target the inner div too just in case */
    .pplr-prev-left {
        transition: all 0.3s ease !important;
    }
}
```
---

### For DOM re-rendering issue while changing the Native Variants
Issued product: https://store.the-ixg.com/products/personalized-door-mat-18x30-gray-bordered-mat?variant=47962275512550 

```jsx
if(!window.Shopify.PaymentButton){
    window.Shopify.PaymentButton = {init: () => {}}
}
const prev_shop_pay_btn_func = window.Shopify.PaymentButton.init;
window.Shopify.PaymentButton.init = () => {
    prev_shop_pay_btn_func()
    jQuery(this).closest('form').css("display", 'block')
    window.pplr_Loaded = false;
    pplr_el = null;
    pplr_tab = '';
    pplr_Ready();
    jQuery(this).closest('form').css("display", 'contents')
}
```

---

### Custom Dev - if anyone wants to user HEX color code while using the Gradient in color set

In CSS - 
```css
/*                                  adding HEX or RGB for radient                                          */


/* ===== 1. Lay out the whole control as a clean horizontal row ===== */
.minicolors.minicolors-theme-default {
  display: inline-flex !important;
  align-items: center !important;
  gap: 8px !important;
  overflow: visible !important;
  position: relative !important;
}

/* ===== 2. The swatch becomes a real, visible color-preview chip ===== */
.minicolors-theme-default .minicolors-swatch {
  position: relative !important;   /* take it OUT of the input's overlay flow */
  top: auto !important;
  left: auto !important;
  width: 32px !important;
  height: 32px !important;
  border: 1px solid #bbb !important;
  border-radius: 4px !important;
  flex: 0 0 auto !important;
  order: 1 !important;             /* chip sits on the LEFT */
  box-shadow: inset 0 0 0 1px rgba(0,0,0,.08) !important;
}
.minicolors-swatch-color {
  border-radius: 3px !important;
}

/* ===== 3. Text input: full readable width, NO padding hack (swatch is separate now) ===== */
.minicolors input.minicolors-input,
input[name="properties[Color Choices]"] {
  display: block !important;
  visibility: visible !important;
  opacity: 1 !important;
  position: relative !important;
  order: 2 !important;             /* input sits in the MIDDLE */
  width: 120px !important;
  height: 32px !important;
  padding: 6px 10px !important;    /* normal padding — swatch no longer overlaps */
  margin: 0 !important;
  font-family: monospace !important;
  font-size: 14px !important;
  color: #222 !important;
  background: #fff !important;
  border: 1px solid #ccc !important;
  border-radius: 4px !important;
  text-transform: uppercase !important;
  z-index: 2 !important;
  cursor: text !important;
  pointer-events: auto !important;
}

/* ===== 4. Picker panel opens to the RIGHT of the row, never covering content ===== */
.minicolors-panel {
  top: 0 !important;
  left: calc(32px + 8px + 120px + 8px) !important;  /* chip + gaps + input + gap */
  right: auto !important;
  bottom: auto !important;
  order: 3 !important;
}

/* ===== 5. Validation feedback ===== */
input[name="properties[Color Choices]"].manual-valid {
  border-color: #4CAF50 !important;
  box-shadow: 0 0 0 2px rgba(76, 175, 80, 0.25) !important;
}
input[name="properties[Color Choices]"].manual-invalid {
  border-color: #f44336 !important;
  box-shadow: 0 0 0 2px rgba(244, 67, 54, 0.25) !important;
}
input[name="properties[Color Choices]"] {
  transition: border-color 0.2s ease, box-shadow 0.2s ease !important;
}


/*----------------------------------------------HEX RGB ended----------------------------------------------------------*/
```

In JS - 
```jsc
// HEX or RGB

(function () {
  const SELECTOR = 'input[name="properties[Color Choices]"]';

  function isValidColor(v) {
    v = v.trim();
    return /^#([0-9A-Fa-f]{3}|[0-9A-Fa-f]{6})$/.test(v) ||
           /^rgba?\(\s*\d{1,3}\s*,\s*\d{1,3}\s*,\s*\d{1,3}\s*(,\s*(0|1|0?\.\d+))?\s*\)$/i.test(v);
  }
  function normalizeHex(v) {
    v = v.trim();
    if (/^#[0-9A-Fa-f]{3}$/.test(v)) return '#' + v[1]+v[1] + v[2]+v[2] + v[3]+v[3];
    return v.toUpperCase();
  }

  function applyLayout(input) {
    const wrap = input.closest('.minicolors');
    if (wrap && !wrap.classList.contains('minicolors-position-right')) {
      wrap.classList.remove('minicolors-position-bottom', 'minicolors-position-top', 'minicolors-position-left');
      wrap.classList.add('minicolors-position-right');
    }
  }

  function syncSwatch(input) {
    // Safety net: ensure the visible chip reflects the current value
    const swatch = input.parentElement.querySelector('.minicolors-swatch-color');
    if (swatch && isValidColor(input.value)) {
      swatch.style.backgroundColor = normalizeHex(input.value);
    }
  }

  function initManualEntry() {
    const input = document.querySelector(SELECTOR);
    if (!input) return;

    applyLayout(input);          // re-apply every pass (survives theme re-init)

    if (input.dataset.manualEntryBound) { syncSwatch(input); return; }
    input.dataset.manualEntryBound = 'true';

    let debounceTimer = null;
    function processManualInput() {
      const raw = input.value.trim();
      if (!raw) { input.classList.remove('manual-valid', 'manual-invalid'); return; }

      const valid = isValidColor(raw);
      input.classList.toggle('manual-valid', valid);
      input.classList.toggle('manual-invalid', !valid);

      if (valid) {
        const normalized = normalizeHex(raw);
        if (typeof jQuery !== 'undefined' && jQuery(input).data('minicolors')) {
          jQuery(input).minicolors('value', normalized);  // updates swatch + grid officially [[1]]
        } else {
          syncSwatch(input);
        }
        if (typeof LoadPplrWithFont === 'function') {
          LoadPplrWithFont(input.dataset.frame, true, input);
        }
      }
    }

    input.addEventListener('input', () => { clearTimeout(debounceTimer); debounceTimer = setTimeout(processManualInput, 300); });
    input.addEventListener('blur',  () => { clearTimeout(debounceTimer); processManualInput(); });
    input.addEventListener('paste', () => { clearTimeout(debounceTimer); setTimeout(processManualInput, 50); });

    // When the PICKER is used (drag/click), keep the chip in sync too
    input.addEventListener('change', () => { applyLayout(input); syncSwatch(input); });

    syncSwatch(input);
  }

  const observer = new MutationObserver(() => initManualEntry());
  observer.observe(document.body, { childList: true, subtree: true, attributes: true, attributeFilter: ['class'] });
  initManualEntry();
})();

// HEX RGB ended
```

---

### Test

```jsx

```
