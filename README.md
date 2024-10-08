# WESTERN GOVERNORS UNIVERSITY 
## D287 – JAVA FRAMEWORKS

## Task Instructions Provided for Reference

Each note should include the prompt, file name, line number, and change.

## Tracked Changes 

C.  Customize the HTML user interface for your customer’s application. The user interface should include the shop name, the product names, and the names of the parts.
Note: Do not remove any elements that were included in the screen. You may add any additional elements you would like or any images, colors, and styles, although it is not required.

<strong>Filename: mainscreen.html</strong>

Line 14: Changed title to Pete's Pressure Washing
```html
<title>Pete's Pressure Washing</title>
```
Line 19: Changed h1 to Pete's Pressure Washing
```html
<h1>Pete's Pressure Washing</h1>
```
Line 21: Changed h2 to Pressure Washing Parts
```html
<h2>Pressure Washing Parts</h2>
```
Line 53: Changed h2 to Pressure Washing Products
```html
<h2>Pressure Washing Products</h2>
```
Lines 91-93: Added a footer
```html
<footer>
    Copyright 2024, Pete's Pressure Washing
</footer>
```
Lines 97-124: Updated CSS Styling
```html
<!--CSS Styling-->
<style>
    * {
        border: 1px solid black;
        align-content: center;
    }

    body {
        background: #DAA520;
        color: #fff;
    }

    .container {
        background: #DAA520;
        color: #0d6efd;
    }

    .footer {
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        background-color: #333;
        color: white;
        text-align: center;
    }

</style>
```

D.  Add an “About” page to the application to describe your chosen customer’s company to web viewers and include navigation to and from the “About” page and the main screen.

<strong>Filename: about.html</strong>

Lines 1-54: Added About.html page with layout and content
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
  <meta charset="UTF-8">

  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

  <title>Pete's Pressure Washing</title>
</head>
<body>
  <div class="container"></div>
   <h1>About Us</h1>
   <a href="mainscreen.html">Back to Main Screen</a>
   <p>Our company has been in business for over 20 years. We specialize in pressure washing parts and products. We have a wide selection of parts and products to choose from. We also offer in house and outsourced parts. Our prices are competitive and our customer service is top-notch. We look forward to doing business with you!</p>
   <h1>Our Products</h1>
   <p>At Pete's Pressure Washing, we are committed to using only the highest quality products, sourced from the best suppliers in the industry. This ensures that every job we undertake is not only completed to the highest standards but also with the most effective and reliable products available.</p>
</body>
</html>
<footer>
    Copyright 2024, Pete's Pressure Washing
</footer>

<!--CSS Styling-->
<style>
  * {
    border: 1px solid black;
  }
  body {
    background: #DAA520;
    color: #fff;
  }

  .container {
    background: #DAA520;
    color: #0d6efd;
  }

  .footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    background-color: #333;
    color: white;
    text-align: center;
  }

</style>
```
Line 19: Updated about.html to include link back to main screen
```html
<a href="mainscreen">Back to Main Screen</a>
```

<strong>Filename: mainscreen.html</strong>

Line 17: Added a link to the about page
```html
<a href="about.html">About Us</a>
```
Line 20: Refined the link to the about page
```html
<a id="aboutbutton" class="btn btn-primary aboutbutton" href="about.html">About Us</a>
```
E.  Add a sample inventory appropriate for your chosen store to the application. You should have five parts and five products in your sample inventory and should not overwrite existing data in the database.
Note: Make sure the sample inventory is added only when both the part and product lists are empty. When adding the sample inventory appropriate for the store, the inventory is stored in a set so duplicate items cannot be added to your products. When duplicate items are added, make a “multi-pack” part.

<strong>Filename: BootStrapData.java</strong>

Lines 27-40: Added a new repo for inhouse parts
```java
@Component
public class BootStrapData implements CommandLineRunner {

    private final PartRepository partRepository;
    private final ProductRepository productRepository;
    private final InhousePartRepository inhousePartRepository;
    private final OutsourcedPartRepository outsourcedPartRepository;

    public BootStrapData(PartRepository partRepository, ProductRepository productRepository, InhousePartRepository inhousePartRepository, OutsourcedPartRepository outsourcedPartRepository) {
        this.partRepository = partRepository;
        this.productRepository = productRepository;
        this.inhousePartRepository = inhousePartRepository;
        this.outsourcedPartRepository = outsourcedPartRepository;
    }
}
```
Lines 35-159: Created 5 parts, 2 Inhouse, and 3 Outsourced

```java
   @Override
public void run(String... args) throws Exception {
    List<InhousePart> inhouseParts = (List<InhousePart>) inhousePartRepository.findAll();

    InhousePart part1 = new InhousePart();
    part1.setId(1);
    part1.setName("Shooter Tips");
    part1.setInv(10);
    part1.setMin(1);
    part1.setMax(50);
    part1.setPrice(50.0);
    inhousePartRepository.save(part1);
    inhouseParts = (List<InhousePart>) inhousePartRepository.findAll();
    InhousePart thePart = null;
    for (InhousePart part : inhouseParts) {
        if (part.getName().equals("Shooter Tip")) {
            thePart = part;
            break;
        }
    }

    if (thePart != null) {
        System.out.println(thePart.getName());
    } else {
        System.out.println("Part not found");
    }

    InhousePart part2 = new InhousePart();
    part2.setId(2);
    part2.setName("Washing Hose");
    part2.setInv(20);
    part2.setMin(1);
    part2.setMax(50);
    part2.setPrice(30.0);
    inhousePartRepository.save(part2);
    inhouseParts = (List<InhousePart>) inhousePartRepository.findAll();
    thePart = null;
    for (InhousePart part : inhouseParts) {
        if (part.getName().equals("Washing Hose")) {
            thePart = part;
            break;
        }
    }

    if (thePart != null) {
        System.out.println(thePart.getName());
    } else {
        System.out.println("Part not found");
    }

    inhouseParts = (List<InhousePart>) inhousePartRepository.findAll();
    for (InhousePart part : inhouseParts) {
        System.out.println(part.getName() + " " + part.getId());
    }

    List<OutsourcedPart> outsourcedParts = (List<OutsourcedPart>) outsourcedPartRepository.findAll();

    OutsourcedPart part3 = new OutsourcedPart();
    part3.setCompanyName("Amazon");
    part3.setId(3);
    part3.setName("Surface Cleaner");
    part3.setInv(5);
    part3.setMin(1);
    part3.setMax(50);
    part3.setPrice(100.0);
    outsourcedPartRepository.save(part3);
    //Update list after saving the new part
    outsourcedParts = (List<OutsourcedPart>) outsourcedPartRepository.findAll();
    OutsourcedPart theOutPart = null;
    for (OutsourcedPart part : outsourcedParts) {
        if (part.getName().equals("Surface Cleaner")) {
            theOutPart = part;
            break;
        }
    }

    if (theOutPart != null) {
        System.out.println(theOutPart.getName());
    } else {
        System.out.println("Part not found");
    }

    OutsourcedPart part4 = new OutsourcedPart();
    part4.setCompanyName("Lowes");
    part4.setId(4);
    part4.setName("Wonder Wand");
    part4.setInv(25);
    part4.setMin(1);
    part4.setMax(50);
    part4.setPrice(50.0);
    outsourcedPartRepository.save(part4);
    //Update list after saving the new part
    outsourcedParts = (List<OutsourcedPart>) outsourcedPartRepository.findAll();
    theOutPart = null;
    for (OutsourcedPart part : outsourcedParts) {
        if (part.getName().equals("Wonder Wand")) {
            theOutPart = part;
            break;
        }
    }

    if (theOutPart != null) {
        System.out.println(theOutPart.getName());
    } else {
        System.out.println("Part not found");
    }

    OutsourcedPart part5 = new OutsourcedPart();
    part5.setCompanyName("Home Depot");
    part5.setId(5);
    part5.setName("Pressure Valve");
    part5.setInv(20);
    part5.setMin(1);
    part5.setMax(50);
    part5.setPrice(15.0);
    outsourcedPartRepository.save(part5);
    outsourcedParts = (List<OutsourcedPart>) outsourcedPartRepository.findAll();
    theOutPart = null;
    for (OutsourcedPart part : outsourcedParts) {
        if (part.getName().equals("Pressure Valve")) {
            theOutPart = part;
            break;
        }
    }

    if (theOutPart != null) {
        System.out.println(thePart.getName());
    } else {
        System.out.println("Part not found");
    }

        /*inhouseParts = (List<InhousePart>) inhousePartRepository.findAll();
        for (InhousePart part : inhouseParts) {
            System.out.println(part.getName() + " " + part.getId());
        }*/

        /*List<OutsourcedPart> outsourcedParts = (List<OutsourcedPart>) outsourcedPartRepository.findAll();
        for (OutsourcedPart part : outsourcedParts) {
            System.out.println(part.getName() + " " + part.getCompanyName());
        }*/
}
 ```
Lines 171-193: Updated BootStrapData.java so that products stopped repeating.
```java
  if (productRepository.count() == 0) {

Product two_gpm_washer = new Product("2 GPM Washer", 100.00, 10);
Product three_gpm_washer= new Product("3 GPM Washer",200.00,10);
Product four_gpm_washer= new Product("4 GPM Washer",300.00,8);
Product five_gpm_washer= new Product("5 GPM Washer",600.00,5);
Product six_gpm_washer= new Product("6 GPM Washer",1000.00,3);

            productRepository.save(two_gpm_washer);
            productRepository.save(three_gpm_washer);
            productRepository.save(four_gpm_washer);
            productRepository.save(five_gpm_washer);
            productRepository.save(six_gpm_washer);

            System.out.println("Started in Bootstrap");
            System.out.println("Number of Products" + productRepository.count());
        System.out.println(productRepository.findAll());
        System.out.println("Number of Parts" + partRepository.count());
        System.out.println(partRepository.findAll());

        }
        }
        }
```

F.  Add a “Buy Now” button to your product list. Your “Buy Now” button must meet each of the following parameters:
•  The “Buy Now” button must be next to the buttons that update and delete products.
•  The button should decrement the inventory of that product by one. It should not affect the inventory of any of the associated parts.
•  Display a message that indicates the success or failure of a purchase.

<strong>Filename: mainscreen.html</strong>

Line 82: Added a Buy Now Button in the product list
```html
<a th:href="@{/buyNow(productID=${tempProduct.id})}" class="btn btn-primary btn-sm mb-3">Buy Now</a>
```

<strong>NEW Filename: BuyingProductController.java</strong>

Lines 1-54: Added BuyingProductController to handle the Buy Now button in the mainscreen.html
```java
@Controller
public class BuyingProductController {
    @Autowired
    private ProductRepository productRepository;

    @GetMapping("/buyProduct")
    public String buyingProduct(@RequestParam("productId") Long productId, Model theModel) {

        Optional<Product> buyingProduct = productRepository.findById(productId);

        if (buyingProduct.isPresent()) {
            Product product = buyingProduct.get();
            theModel.addAttribute("product", product);
            if (product.getInv() > 0) {
                product.setInv(product.getInv() - 1);
                productRepository.save(product);
                return "/buyingSuccess";
            } else {
                return "/buyingFail";
            }
        } else {
            return "/buyingFail";
        }
    }
}
```
Lines 13-37 updated BuyingProductController.java
```java
@Controller
public class BuyingProductController {
    @Autowired
    private ProductRepository productRepository;

    @GetMapping("/buyProduct")
    public String buyProduct(@RequestParam("productID") Long theId, Model Model) {
        Optional<Product> productBuying = productRepository.findById(theId);

        if (productBuying.isPresent()) {    //check if product in catalog
            Product product = productBuying.get();

            if (product.getInv() > 0) {
                product.setInv(product.getInv() - 1);
                productRepository.save(product);

                return "/buyingSuccess";
            } else {
                return "/buyingFail";
            }
        } else {
            return "/buyingFail";
        }
    }
}
```

<strong>NEW Filename: buyingSuccess.html</strong>
Lines 1-11: Added a buyingSuccess.html file to output a statement if purchase is successful.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>buyingSuccess</title>
</head>
<body>
<a id="mainscreen" class="btn btn-primary mainscreen" href="mainscreen">Back to Mainscreen</a>
<p>Your purchase was successful! We thank you for your purchase and hope to see you again soon.</p>
</body>
</html>
```

<strong>NEW Filename: buyingFail.html</strong>

Lines 1-11: Added a buyingFail.html file to output a statement if purchase is a failure.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>buyingFail</title>
</head>
<body>
<a id="mainscreen" class="btn btn-primary mainscreen" href="mainscreen">Back to Mainscreen</a>
<p>Your purchase did not succeed. Please ensure the product is not in stock and contact us if needed!</p>
</body>
</html>
```
G.  Modify the parts to track maximum and minimum inventory by doing the following:
•  Add additional fields to the part entity for maximum and minimum inventory.
•  Modify the sample inventory to include the maximum and minimum fields.
•  Add to the InhousePartForm and OutsourcedPartForm forms additional text inputs for the inventory so the user can set the maximum and minimum values.
•  Rename the file the persistent storage is saved to.
•  Modify the code to enforce that the inventory is between or at the minimum and maximum value.

<strong> Filename: part.java</strong>

Lines 31-34: Added a min and max for minInv and maxInv respectively.
```java
 @Min(value = 0, message = "Minimum inventory value must be positive")
int minInv;
@Max(value = 100, message = "Maximum inventory value must fall within set maximum")
int maxInv;
```

Lines 44-59: Added minInv and maxInv to two constructors and set initial values.
```java
 public Part(String name, double price, int inv) {
    this.name = name;
    this.price = price;
    this.inv = inv;
    this.minInv = 0;
    this.maxInv = 100;
}

public Part(long id, String name, double price, int inv, int minInv, int maxInv) {
    this.id = id;
    this.name = name;
    this.price = price;
    this.inv = inv;
    this.minInv = minInv;
    this.maxInv = maxInv;
}
```

Lines 101-111: Created a new getter and setter for both minInv and maxInv.
```java
 public int getMinInv() {
    return minInv;
}

public void setMin(int minInv) { this.minInv = minInv; }

public int getMaxInv() {
    return maxInv;
}

public void setMax(int maxInv) { this.maxInv = maxInv; }
```

Updated lines 135-141: Created a method to check if inv is below or above the min and max.
```java
     public void validateLimits() {
    if (this.inv < this.minInv) {
        throw new RuntimeException("Inventory is below minimum: " + this.minInv);
    } else if (this.inv > this.maxInv) {
        throw new RuntimeException("Inventory is above maximum: " + this.maxInv);
    }
}
```

<strong>Filename: BootStrapData.java.java</strong>

Lines 44-45, 67-68, 98-99, 123-124, 148, 149: Set, setmin = 1 and setMax = 100 for all parts.
```java
*.setMin(1);
*.setMax(100);
```

<strong>Filename: InhousePart.java</strong>

Lines 17-20: Added minInv and maxInv values.
```java
public InhousePart() {
    this.minInv = 0;
    this.maxInv = 100;
}
```

<strong>Filename: OutsourcedPart.java</strong>

Lines 18-21: Added minInv and maxInv values.
```java
    public OutsourcedPart() {
    this.minInv = 0;
    this.maxInv = 100;
}
```

<strong>Filename: InhousePartForm.html</strong>

Lines 25-29 added fields for the user to input min and max values.
```html
<p><input type="text" th:field="*{minInv}" placeholder="Minimum Inventory" class="form-control mb-4 col-4"/></p>
<p th:if="${#fields.hasErrors('valMin')}" th:errors="*{minInv}">Minimum Inventory Error</p>

<p><input type="text" th:field="*{maxInv}" placeholder="Maximum Inventory" class="form-control mb-4 col-4"/></p>
<p th:if="${#fields.hasErrors('valMax')}" th:errors="*{maxInv}">Maximum Inventory Error</p>
```

<strong>Filename: OutsourcedPartForm.html</strong>

Lines 25-29 added fields for the user to input min and max values.
```html
<p><input type="text" th:field="*{minInv}" placeholder="Minimum Inventory" class="form-control mb-4 col-4"/></p>
<p th:if="${#fields.hasErrors('minInv')}" th:errors="*{minInv}">Minimum Inventory Error</p>

<p><input type="text" th:field="*{maxInv}" placeholder="Maximum Inventory" class="form-control mb-4 col-4"/></p>
<p th:if="${#fields.hasErrors('maxInv')}" th:errors="*{maxInv}">Maximum Inventory Error</p>
```

<strong>Filename: application.properties</strong>

Lines 6 chagned location of data file to petes-pressure-washing-db.
```html
spring.datasource.url=jdbc:h2:file:~/petes-pressure-washing-db
```

<strong>Filename: PartServiceImpl.java</strong>

Updated lines 57-62: Added limits method check prior to partRepository.save.
```java
    @Override
    public void save(Part thePart) {
            thePart.validateInventory();
            partRepository.save(thePart);

    }
```

<strong>Filename: InhousePartServiceImpl.java</strong>

Updated lines 52-57: Added limits method check prior to partRepository.save.
```java
    @Override
    public void save(InhousePart thePart) {
        thePart.validateInventory();
        partRepository.save(thePart);

    }
```

<strong>Filename: OutsourcedPartServiceImpl.java</strong>

Updated lines 50-55: Added limits method check prior to partRepository.save.
```java
@Override 
  public void save(OutsourcedPart thePart) {
    thePart.validateInventory();
    partRepository.save(thePart);

}
```

<strong>Filename: mainscreen.html</strong>

Lines 48-49 added min and max fields so that they are displayed in main screen.
```html
           <td th:text="${tempPart.minInv}">1</td>
<td th:text="${tempPart.maxInv}">1</td>
```

H.  Add validation for between or at the maximum and minimum fields. The validation must include the following:
•  Display error messages for low inventory when adding and updating parts if the inventory is less than the minimum number of parts.
•  Display error messages for low inventory when adding and updating products lowers the part inventory below the minimum.
•  Display error messages when adding and updating parts if the inventory is greater than the maximum.

<strong>Filename: ValidMin.java</strong>

Lines 1-24: Added a ValidMin validator to throw an error message when parts drop below the minimum inventory.
```java
package com.example.demo.validators;

import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 *
 *
 *
 *
 */
@Constraint(validatedBy = {ValidMinValidator.class})
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidMin {
    String message() default "Inventory falls below the minimum inventory!";
    Class<?> [] groups() default {};
    Class<? extends Payload> [] payload() default {};

}
```

<strong>Filename: ValidMinValidator.java</strong>

Lines 1-29: If statement that checks if part is below minimum and passes that to ValidMin.
```java
package com.example.demo.validators;

import com.example.demo.domain.Part;
import com.example.demo.domain.Product;

import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

/**
 *
 *
 *
 *
 */
public class ValidMinValidator implements ConstraintValidator<ValidMin, Part> {
    @Override
    public void initialize(ValidMin constraintAnnotation) {
        ConstraintValidator.super.initialize(constraintAnnotation);
    }

    @Override
    public boolean isValid(Part part, ConstraintValidatorContext constraintValidatorContext) {
        if (part.getInv() > part.getMinInv()) {
            return true;
        } else {
            return false;
        }
    }
}
```

<strong>Filename: Part.java</strong>

Lines 3 and 18: imported and called validator.ValidMin.
```java
import com.example.demo.validators.ValidMin;

@ValidMin
```

<strong>Filename: EnufPartsValidator.java</strong>

Lines 28-48: Updated EnufPartValidator to throw a custom constraint if product inventory falls below minimum.
```java
    @Override
    public boolean isValid(Product product, ConstraintValidatorContext constraintValidatorContext) {
        if(context==null) return true;
        if(context!=null)myContext=context;
        ProductService repo = myContext.getBean(ProductServiceImpl.class);
        if (product.getId() != 0) {
            Product myProduct = repo.findById((int) product.getId());
            for (Part p : myProduct.getParts()) {
                if (p.getInv()<(product.getInv()-myProduct.getInv())) {
                    constraintValidatorContext.disableDefaultConstraintViolation();
                    constraintValidatorContext.buildConstraintViolationWithTemplate("Inventory level of part " + p.getName() + " is insufficient.").addConstraintViolation();
                    return false;
                }
            }
            return true;
        }
        else{
                return true;
            }
    }
}
```

<strong>Filename: ValidMax.java</strong>

Lines 1-24: Added a ValidMax validator to throw an error message when parts rise above the maximum.
```java
package com.example.demo.validators;

import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 *
 *
 *
 *
 */
@Constraint(validatedBy = {ValidMaxValidator.class})
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidMax {
    String message() default "Inventory goes above the maximum inventory!";
    Class<?> [] groups() default {};
    Class<? extends Payload> [] payload() default {};

}
```

<strong>Filename: ValidMaxValidator.java</strong>

Lines 1-29: If statement that checks if part is above maximum and passes that to ValidMax.
```java
package com.example.demo.validators;

import com.example.demo.domain.Part;
import com.example.demo.domain.Product;

import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

/**
 *
 *
 *
 *
 */
public class ValidMaxValidator implements ConstraintValidator<ValidMax, Part> {
    @Override
    public void initialize(ValidMax constraintAnnotation) {
        ConstraintValidator.super.initialize(constraintAnnotation);
    }

    @Override
    public boolean isValid(Part part, ConstraintValidatorContext constraintValidatorContext) {
        if (part.getInv() > part.getMaxInv()) {
            return false;
        } else {
            return true;
        }
    }
}
```

<strong>Filename: Part.java</strong>

Lines 4 and 20: imported and called validator.ValidMax.
```java
import com.example.demo.validators.ValidMax;

@ValidMax
```
I.  Add at least two unit tests for the maximum and minimum fields to the PartTest class in the test package.

<strong>Filename: PartTest.java</strong>

Lines 160-194: Added four unit tests for minimum and maximum inventory fields.
```java
@Test
    void setMin() {
        int minInv = 1;
        partIn.setMin(minInv);
        assertEquals(minInv,partIn.getMinInv());
        partOut.setMin(minInv);
        assertEquals(minInv,partOut.getMinInv());
    }

    @Test
    void getMinInv() {
        int minInv = 1;
        partIn.setMin(minInv);
        assertEquals(minInv,partIn.getMinInv());
        partOut.setMin(minInv);
        assertEquals(minInv,partOut.getMinInv());
    }

    @Test
    void setMax() {
        int maxInv = 200;
        partIn.setMax(maxInv);
        assertEquals(maxInv,partIn.getMaxInv());
        partOut.setMax(maxInv);
        assertEquals(maxInv,partOut.getMaxInv());
    }

    @Test
    void getMaxInv() {
        int maxInv = 200;
        partIn.setMax(maxInv);
        assertEquals(maxInv,partIn.getMaxInv());
        partOut.setMax(maxInv);
        assertEquals(maxInv,partOut.getMaxInv());
    }
```

J.  Remove the class files for any unused validators in order to clean your code.

Deleted unused validators: <strong>Filename: DeletePartValidator</strong>
Deleted unused validators: <strong>Filename: ValidDeletePart</strong>

K.  Demonstrate professional communication in the content and presentation of your submission.


## File Restrictions
File name may contain only letters, numbers, spaces, and these symbols: ! - _ . * ' ( )
File size limit: 200 MB
File types allowed: doc, docx, rtf, xls, xlsx, ppt, pptx, odt, pdf, csv, txt, qt, mov, mpg, avi, mp3, wav, mp4, wma, flv, asf, mpeg, wmv, m4v, svg, tif, tiff, jpeg, jpg, gif, png, zip, rar, tar, 7z