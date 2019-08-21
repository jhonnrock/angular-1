## Angular 8 Cheat Sheet created during work hours

This part will be updated later 

## Displaying Data

### The code in component file
``` javascript
export class Component {
  title = 'Angular Cheat Sheet';
  languages = ['Javascript', 'PHP', 'Python', 'C++'];
  age = 18;
}
```

### The code in the HTML file

``` html

## Showing component properties with interpolation
<div> {{ title }} </div>

## Showing an array property with *ngFor
<ul>
  <li *ngFor="let language of languages">
    {{ language }}
  </li>
</ul>

## Conditional display with NgIf
<p *ngIf="age > 18">You are allowed to enter the club!</p>

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
