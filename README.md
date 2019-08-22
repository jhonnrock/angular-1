# Angular 8 Cheat Sheet created during work hours
### [Live Demo](https://angular-chsh.netlify.com)

_**This part will be updated later**_ 
_Using Bootstrap classes in HTML files_


# Displaying Data
display-data.component.ts
``` javascript
export class DisplayDataComponent {
  title = 'Angular Cheat Sheet';
  languages = ['Javascript', 'PHP', 'Python', 'C++'];
  age = 19;
}
```

display-data.component.html
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

template-statements.component.ts
``` javascript
export class TemplateStatementsComponent {

  likes = 10;
  liked: boolean;

  like(): void {
    this.likes += (this.liked) ? -1 : 1;
    this.liked = !this.liked;
  }

}
```

template-statements.component.html
<!-- {% raw %} -->
``` html
<div class="card" style="max-width: 400px">
  <div class="card-body p-4">
    Lorem ipsum dolor sit amet, consec tetur adipi scing elit. Pellen tesque
    vesti bulum id libero sollici tudin iaculis.
  </div>
  <div class="card-footer">
    <span class="h3" (click)="like()">
      <i class="fas fa-heart"
        [ngClass]="this.liked ? 'text-danger' : 'text-secondary'">
      </i>
    </span>
    <span class="h3"> {{ likes }} </span> Likes
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
    id: number;
    name: string;
    rating: number;

    constructor(id: number, name: string, rating: number) {
        this.id = id;
        this.name = name;
        this.rating = rating;
    }
}
```

### Parent Component
courses.component.ts
``` javascript
import {Course} from '../course.model';

export class CoursesComponent {
  addedCourses = [];

  courses = [
    new Course(1, 'Master Angular', 8),
    new Course(2, 'Master Laravel', 7),
    new Course(3, 'Master ReactJS', 6)
  ];

  onBuyCourse(course: Course) {
    if (!this.addedCourses.includes(course)) {
      this.addedCourses.push(course);
    }
  }

  remove(course: number) {
    this.addedCourses = this.addedCourses.filter(
      (item) => return item !== course;
    );
  }
```

courses.component.html
<!-- {% raw %} -->
```html
<div class="row mt-4">
  <app-course-item
    *ngFor="let course of courses"
    [courseData]="course"
    (boughtCourse)="onBuyCourse($event)"
    class="col-xs-12 col-sm-6 col-md-3"
  >
  </app-course-item>
  <div class="col-3" *ngIf="addedCourses.length > 0">
    <h4>Bought Courses</h4>
    <ul class="list-group">
      <li class="list-group-item" *ngFor="let addedCourse of addedCourses">
        <div class="row justify-content-between align-items-center">
          {{ addedCourse.name }}
          <button class="btn btn-danger" (click)="remove(addedCourse)">
            <i class="fas fa-times"></i>
          </button>
        </div>
      </li>
    </ul>
  </div>
</div>
```
<!-- {% endraw %} -->


### Child Component

course-item.component.ts
``` javascript
import { Course } from '../course.model';
export class CourseItemComponent {

  @Input() courseData: Course;
  @Output() boughtCourse = new EventEmitter<Course>();

  buyCourse(course: Course) {
    this.boughtCourse.emit(course);
  }

}
```

course-item.component.html
<!-- {% raw %} -->
``` html
<div class="card mb-2">
  <div class="card-body h3 text-center">
    {{ courseData.name }}
  </div>
  <div class="card-footer">
    <div class="row justify-content-between">
      <button class="btn btn-primary" (click)="buyCourse(courseData)">
        Buy
      </button>
      <span class="ml-2 btn btn-warning"> {{ courseData.rating }} ★ </span>
    </div>
  </div>
</div>
```
<!-- {% endraw %} -->

### Screenshot
![Component Intercation](https://raw.githubusercontent.com/eneajaho/angular/master/img/3.png)


# Template-driven Forms

template-form.component.ts
``` javascript
export class TemplateFormComponent {

  submitedData;

  categories = [
    { id: 1, name: 'Teacher' },
    { id: 2, name: 'Developer' },
    { id: 3, name: 'Chef' }
  ];

  submit(formInput) {
    this.submitedData = formInput;
  }

}

```
template-form.component.html
<!-- {% raw %} -->
``` html
<div class="row">
  <div class="col-md-6 col-xs-12">
    <div class="card">
      <div class="card-body">
        <form #f="ngForm" (ngSubmit)="submit(f.value)">
          <div class="form-group">
            <label for="course"> Course Name </label>
            <input required ngModel name="course" #course="ngModel"
              id="course"
              type="text"
              class="form-control"/>
            <div
              class="alert alert-danger mt-1"
              *ngIf="course.touched && course.invalid">
              <div *ngIf="course.errors.required">Course Name is required.</div>
            </div>
          </div>

          <div class="form-group">
            <label for="category">Category</label>
            <select
              required
              ngModel
              name="category"
              #category="ngModel"
              id="category"
              class="form-control">
              <option value=""></option>
              <option *ngFor="let category of categories" [value]="category.id">
                {{ category.name }}
              </option>
            </select>

            <div
              *ngIf="category.touched && category.invalid"
              class="alert alert-danger">
              Category Field is required
            </div>
          </div>

          <div class="checkbox mb-4">
            <label for="checkbox"> </label>
            <input ngModel name="checkbox" type="checkbox" id="checkbox" />
            Agree to license terms?
          </div>
          <button [disabled]="f.invalid" class="btn btn-primary">Create</button>
        </form>
      </div>
    </div>
  </div>
  <div class="col-md-6 col-xs-12" *ngIf="submitedData">
    <h4>Submited Data</h4>
    <div class="card p-4">
      <pre> {{ submitedData | json }}</pre>
    </div>
  </div>
</div>
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
