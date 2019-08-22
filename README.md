# Angular 8 Cheat Sheet created during work hours

_**This part will be updated later**_ 
_Using Bootstrap classes in HTML files_


# Displaying Data

The code in component.ts file
``` javascript
export class Component {
  title = 'Angular Cheat Sheet';
  languages = ['Javascript', 'PHP', 'Python', 'C++'];
  age = 19;
}
```

The code in the HTML file
<!-- {% raw %} -->
``` html
### Showing component properties with interpolation
<h1> {{ title }} </h1>

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


### Screenshot
![Displaying Data in Angular](https://raw.githubusercontent.com/eneajaho/angular/master/img/1.png)


# Template statements

The code in component.ts file
``` javascript
export class Component {

  likes = 10;
  liked: boolean;

  like() {
    this.likes += (this.liked) ? -1 : 1;
    this.liked = !this.liked;
  }
}
```

The code in the HTML file
<!-- {% raw %} -->
``` html
<div class="card">
    <div class="card-body">
        Lorem ipsum dolor sit amet, consec tetur adipi scing elit.
        Pellen tesque vesti bulum id libero sollici tudin iaculis.
    </div>
    <div class="card-footer">
        ### On Click event execute the like() function
        <span class="h3" (click)="like()">
          <i class="fas fa-heart" [ngClass]="this.liked === true ? 'text-danger' : 'text-secondary'"></i>
        </span>
        <span class="h3">  {{ likes }} </span> Likes
    </div>
</div>
```
<!-- {% endraw %} -->

### Screenshot
![Template statements](https://raw.githubusercontent.com/eneajaho/angular/master/img/2.png)


# Component Interaction 
**Passing data from parent to child component and backwards**

**Creating a class for later use**
```javascript
export class Course {
    name: string;
    rating: number;
    
    constructor(name: string, rating: number) {
        this.name = name;
        this.rating = rating;
    }
}
```

### Parent Component
The code in parentComponent.ts file
``` javascript
import {Course} from '../course.model';

export class ParentComponent {
  addedCourses = [];

  courses = [
    new Course('Master Angular', 8),
    new Course('Master Laravel', 7),
    new Course('Master ReactJS', 6)
  ];

  onBuyCourse(course: Course) {
    this.addedCourses.push(course);
  }
  
}
```

The code in the parent HTML file
<!-- {% raw %} -->
```html
<div class="row mt-5">
  <course-item
    *ngFor="let course of courses"
    [courseData]="course"
    (boughtCourse)="onBuyCourse($event)"
    class="col-3">
  </course-item>
</div>
```
<!-- {% endraw %} -->


### Child Component

The code in childComponent.ts file
``` javascript
export class ChildComponent {
  @Input() courseData: Course;
  @Output() boughtCourse: new EventEmitter<Course>(); 
  
  buyCourse(course) {
    this.boughtCourse.emit(course);
  }
}
```

The code in the child HTML file
<!-- {% raw %} -->
``` html
<div class="card">
  <div class="card-body h3 text-center">
    {{ courseData.name }}
  </div>
  <div class="card-footer">
    <div class="row justify-content-between">
      <button
          class="btn btn-primary"
          (click)="buyCourse(courseData)">
        Buy
      </button>
      <span class="btn btn-warning">
        {{ courseData.rating }} ★
      </span>
    </div>
  </div>
</div>
```
<!-- {% endraw %} -->

### Screenshot
![Component Intercation](https://raw.githubusercontent.com/eneajaho/angular/master/img/3.png)


# Template-driven Forms

The code in component.ts file
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
The code in HTML file 
<!-- {% raw %} -->
``` html
### using #f="ngForm"  and (ngSubmit)="submit(f.value)" to submit form data
<form #f="ngForm" (ngSubmit)="submit(f.value)">
    <div class="form-group">
        <label for="course"> Course Name </label>
      
        ### Using ngModel name="course" #course="ngModel" to get data and input changes
        <input 
           required ngModel name="course" #course="ngModel" 
           id="course" type="text" class="form-control">
      
        ### Showing errors using classes that Angular adds in HTML elements
        <div class="alert alert-danger" *ngIf="course.touched && course.invalid">
          <div *ngIf="course.errors.required">Course Name is required.</div>
        </div>
    </div>
  
    <div class="form-group">
        <label for="category">Category</label>
        <select 
            required ngModel name="category" #category="ngModel" 
            id="category" class="form-control">
            <option value=""></option>
          
            ### Looping through categories and binding data to value attribute
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
    
    ### Showing data to view in json format using json pipe
    <p> {{ f.value | json }}  </p>

    ### Adds disabled attribute to button if form is invalid
    <button [disabled]="f.invalid" class="btn btn-primary">Create</button>

</form>

```
<!-- {% endraw %} -->


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


**Thanks for reading!**
