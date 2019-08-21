# Angular 8 Cheat Sheet created during work hours

This part will be updated later 

## Displaying Data

### The code in component.ts file
``` javascript
export class Component {
  title = 'Angular Cheat Sheet';
  languages = ['Javascript', 'PHP', 'Python', 'C++'];
  age = 18;
}
```

### The code in the HTML file
<!-- {% raw %} -->
``` html

### Showing component properties with interpolation
<div> {{ title }} </div>

### Showing an array property with *ngFor
<ul>
  <li *ngFor="let language of languages">
    {{ language }}
  </li>
</ul>

### Conditional display with NgIf
<p *ngIf="age > 18">You are allowed to enter the club!</p>

```
<!-- {% endraw %} -->



## Template-driven Forms

### The code in component.ts file
``` javascript
export class Component {
  categories = [
    {id: 1, name: 'Teacher'},
    {id: 2, name: 'Developer'},
    {id: 3, name: 'Chef'}
  ];
  
  submit(formInput) {
    console.log(formInput);
  }
}
```
### The code in HTML file 
_Using Bootstrap classes_
``` html
<form #f="ngForm" (ngSubmit)="submit(f.value)">
    <div class="form-group">
        <label for="name"> Course Name </label>
        <input 
           required ngModel name="name" #name="ngModel" 
           id="name" type="text" class="form-control">
        <div class="alert alert-danger" *ngIf="name.touched && name.invalid">
          <div *ngIf="name.errors.required">Course Name is required.</div>
        </div>
    </div>
  
    <div class="form-group">
        <label for="category">Category</label>
        <select 
            required ngModel name="category" #category="ngModel" 
            id="category" class="form-control">
            <option value=""></option>
            <option *ngFor="let category of categories" [value]="category.id"> 
                {{ category.name }}
            </option>
        </select>
        
        <div *ngIf="category.touched && category.invalid" class="alert alert-danger">
            Category Field is required
        </div>
    </div>

    <div class="checkbox mb-4">
        <label for="checkbox"> </label>
        <input ngModel name="checkbox" type="checkbox" id="checkbox">
        Agree to license terms?
    </div>

    <p> {{ f.value | json }}  </p>

    <button [disabled]="f.invalid" class="btn btn-primary">Create</button>

</form>

```



```markdown

Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/eneajaho/angular-chsh/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
