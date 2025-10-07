# 🖼️ Oracle APEX — Display Image at Runtime (Show Selected Image in Page Item)

- This guide explains how to display an image dynamically at runtime in an Oracle APEX page item after selecting a file from a File Browse item.
- The selected image will instantly appear in a Display Image item before submission.

## ⚙️ Step 1: Create the Display Image Page Item

- Create a new Page Item with the following properties:

 - Property	Value
 - Name	P6_DISPLAY_IMAGE
 - Type	Display Image
 - Label	(Leave Blank)
 - Based On	Image URL Stored in the Page Item Value
 - Template	Optional
 - Custom Attributes	style="border:1px solid gray;width:120px;height:120px;"
 - Default → Type	Static
 - Static Value	'' (empty)

This item will display the selected image preview on the page.

## 🧩 Step 2: Create the File Browse Item

Create another Page Item to allow the user to select an image file.

 - Property	Value
 - Name	P6_EMP_PHOTO
 - Type	File Browse
 - Storage Type	BLOB column / N/A (for preview only)
 - Accept File Types	image/*

This item will serve as the input source for reading and displaying the image.

## 🧠 Step 3: Add JavaScript Function

- Add the following JavaScript code under Page → Function and Global Variable Declaration section.
- 
```javaScript
// ✅ JavaScript to Display Selected Image at Runtime in Oracle APEX

function readURL(input) {  
    if (input.files && input.files[0] && input.files[0].type.match('image.*')) {  
        var reader = new FileReader();  

        reader.onload = function (e) {  
            // Set the image source dynamically
            $('#P6_DISPLAY_IMAGE').attr('src', e.target.result);  
        }  

        try {  
            reader.readAsDataURL(input.files[0]);  
        }  
        catch(err) {  
            alert("Error: " + err.message);  
        }   
    }  
}  

// Bind file change event to the file browse item
$("#P6_EMP_PHOTO").change(function(){  
    readURL(this);  
});  


```

## 💡 Notes

- This script does not upload the image to the database — it only shows a preview before saving.

- To store the image in a table, use BLOB columns and APEX’s built-in File Browse handling or a custom PL/SQL process.

- You can adjust preview size by changing the CSS width/height in:
  
```css
style="border:1px solid gray;width:120px;height:120px;"

```

- The same logic works for any page item prefix, e.g., P10_, P12_, etc.

 # Thank you
 ## Sanjay Sikder

 You can connect with me on [LinkedIn](https://www.linkedin.com/in/sanjay-sikder/)!
