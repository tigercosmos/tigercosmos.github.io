---
title: Angular 2 表單
date: 2016-12-21 23:46:52
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<p>Angular &#x6846;&#x67B6;&#x4EF0;&#x8CF4;&#x8457; HTML 5 &#x5F37;&#x5927;&#x7684;&#x529F;&#x80FD;&#xFF0C;&#x672C;&#x8EAB;&#x5DF2;&#x7D93;&#x5305;&#x62EC;&#x96D9;&#x5411;&#x7D81;&#x5B9A;&#x3001;&#x8B8A;&#x5316;&#x8DDF;&#x8E2A;&#x3001;&#x9A57;&#x8B49;&#x3001;&#x932F;&#x8AA4;&#x8655;&#x7406;&#x7B49;&#x529F;&#x80FD;&#x3002;<br>
&#x53EF;&#x4EE5;&#x8655;&#x7406;&#xFF1A;</p>
<ul>
<li>Component &#x548C; Template &#x69CB;&#x5EFA;&#x8868;&#x55AE;</li>
<li>&#x96D9;&#x5411;&#x7D81;&#x5B9A;<code>[(ngModel)]</code>&#x8B80;&#x5BEB;&#x8868;&#x55AE;&#x8868;&#x3002;</li>
<li>
<code>ngControl</code>&#x8FFD;&#x8E64;&#x8868;&#x55AE;&#x72C0;&#x614B;&#x548C;&#x6709;&#x6548;&#x6027;&#x3002;</li>
<li>&#x6839;&#x64DA;<code>ngControl</code>&#x6539;&#x8B8A; CSS&#x3002;</li>
<li>&#x986F;&#x793A;&#x9A57;&#x8B49;&#x932F;&#x8AA4;&#x6D88;&#x606F;&#x4E26;&#x555F;&#x7528;/&#x7981;&#x6B62;&#x8868;&#x55AE;&#x3002;</li>
<li>&#x4F7F;&#x7528;&#x672C;&#x5730;&#x6A21;&#x677F;&#x8B8A;&#x91CF;&#x5171;&#x4EAB;&#x63A7;&#x5236;&#x9593;&#x7684;&#x4FE1;&#x606F;&#x3002;</li>
</ul>
<h2>&#x7C21;&#x55AE;&#x7248;</h2>
<pre><code>// app.simpleform.html

 &lt;!-- &#x9019;&#x908A;&#x6709;&#x7528; Bootstrap CSS &#x5537;&#xFF01; --&gt;
 &lt;div class=&quot;jumbotron&quot;&gt;
    &lt;h2&gt;Template Driven Form&lt;/h2&gt;
     &lt;!-- &#x9019;&#x908A;&#x6211;&#x5011;&#x5BA3;&#x544A;&#x4E00;&#x500B;&#x5340;&#x57DF;&#x8B8A;&#x6578; &quot;form&quot; &#x4E26;&#x8B93;&#x5B83;&#x8B8A;&#x6210; ngForm &#x7684;&#x5BE6;&#x4F8B;&#x3002;&#x9019;&#x6A23;&#x5B50;&#x53EF;&#x4EE5;&#x8B93; &quot;form&quot; &#x4F7F;&#x7528; FormGroup&#x7684; API&#xFF0C;&#x6211;&#x5011;&#x5C31;&#x80FD;&#x5920;&#x7528; ngSubmit &#x9001;&#x51FA; form.value &#x8868;&#x683C;&#x7684;&#x503C;&#x3002;--&gt;
    &lt;form #form=&quot;ngForm&quot; (ngSubmit)=&quot;submitForm(form.value)&quot;&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;First Name:&lt;/label&gt;
        &lt;!-- &#x9019;&#x908A;&#x7684; ngModal &#x662F;&#x55AE;&#x5411;&#x7D81;&#x5B9A;&#xFF0C;&#x53EA;&#x6703;&#x9001;&#x8CC7;&#x6599;&#x56DE;&#x53BB;&#x3002;&#x7576;&#x7136;&#x6211;&#x5011;&#x4E5F;&#x53EF;&#x4EE5;&#x7528; [(ngModal)] &#x4F86;&#x96D9;&#x5411;&#x7D81;&#x5B9A;&#x8868;&#x683C;&#x7684;&#x503C; --&gt;
        &lt;input type=&quot;text&quot; class=&quot;form-control&quot; placeholder=&quot;John&quot; name=&quot;firstName&quot; ngModel required&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Last Name&lt;/label&gt;
        &lt;input type=&quot;text&quot; class=&quot;form-control&quot; placeholder=&quot;Doe&quot; name=&quot;lastName&quot; ngModel required&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Gender&lt;/label&gt;
      &lt;/div&gt;
      &lt;!-- Radio &#x548C; checkbox &#x8DDF;&#x4E00;&#x822C;&#x7684; HTML&#x7528;&#x6CD5;&#x5DEE;&#x4E0D;&#x591A; --&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Male&quot; ngModel&gt;
          Male
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Female&quot; ngModel&gt;
          Female
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Activities&lt;/label&gt;
      &lt;/div&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;hiking&quot; name=&quot;hiking&quot; ngModel&gt; 
        Hiking
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;swimming&quot; name=&quot;swimming&quot; ngModel&gt; 
        Swimming
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;running&quot; name=&quot;running&quot; ngModel&gt; 
        Running
      &lt;/label&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;button type=&quot;submit&quot; class=&quot;btn btn-default&quot;&gt;Submit&lt;/button&gt;
      &lt;/div&gt;
    &lt;/form&gt;
  &lt;/div&gt;
</code></pre>
<pre><code>// app.simpleform.ts

import { Component } from &apos;@angular/core&apos;;

@Component({
  selector: &apos;simple-form&apos;,
  templateUrl: &apos;app.simpleform.html&apos;
})
export class SimpleFormComponent {
  //&#x9019;&#x908A;&#x8A2D;&#x5B9A;&#x63D0;&#x4EA4;&#x5F8C;&#x8981;&#x5E79;&#x561B;&#xFF0C;&#x76EE;&#x524D;&#x53EA;&#x662F; Console.log &#x51FA;&#x8CC7;&#x6599;&#x800C;&#x5DF2;
  submitForm(form: any): void{
    console.log(&apos;Form Data: &apos;);
    console.log(form);
  }
}
</code></pre>
<p>&#x7A0B;&#x5F0F;&#x78BC;&#x5C31;&#x4E0D;&#x591A;&#x89E3;&#x91CB;&#xFF0C;&#x90FD;&#x6709;&#x52A0;&#x8A3B;&#x89E3;&#xFF0C;&#x6B64;&#x5916; <code>required</code> &#x6703;&#x5F37;&#x5236;&#x8981;&#x6C42;&#x4F7F;&#x7528;&#x8005;&#x8F38;&#x5165;&#xFF0C;&#x5426;&#x5247;&#x5C31;&#x6703;&#x7121;&#x6CD5;&#x63D0;&#x4EA4;&#x3002;<br>
&#x4E0A;&#x9762;&#x7684;&#x7BC4;&#x4F8B;&#x6703;&#x9577;&#x5F97;&#x50CF;&#x9019;&#x6A23;<br>
<img src="https://cdn.scotch.io/4/HQ1ZPzHwS2m14nUTCBvV_Screen%20Shot%202016-09-21%20at%203.36.18%20PM.png" alt></p>
<h2>&#x8907;&#x96DC;&#x4E00;&#x9EDE;&#x9EDE;&#x7248;&#x672C;</h2>
<p>&#x597D;&#x7684;&#x4F8B;&#x5B50;&#x52DD;&#x904E;&#x842C;&#x8A00;</p>
<pre><code>// app.complexform.ts

import { Component } from &apos;@angular/core&apos;;
// &#x9700;&#x8981;&#x5F15;&#x5165;&#x4E00;&#x4E9B;&#x7A0B;&#x5F0F;&#x5EAB;
import { FormBuilder, FormGroup } from &apos;@angular/forms&apos;;

@Component({
  selector: &apos;complex-form&apos;,
  templateUrl : &apos;./app.complexform.html&apos;
})
export class ComplexFormComponent {
  // &#x65B0;&#x5EFA;&#x4E00;&#x500B; FormGroup &#x7269;&#x4EF6;
  complexForm : FormGroup;

  // &#x5EFA;&#x69CB;&#x4E00;&#x500B;&#x5BE6;&#x4F8B; FormBuilder
  constructor(fb: FormBuilder){
    // &#x7528; FormBuilder &#x4F86;&#x88FD;&#x9020;&#x6211;&#x5011;&#x7684;&#x8868;&#x683C;
    this.complexForm = fb.group({
      // &#x5B9A;&#x7FA9;&#x8868;&#x683C;&#x7684;&#x9810;&#x8A2D;&#x503C;
      &apos;firstName&apos; : &apos;&apos;,
      &apos;lastName&apos;: &apos;&apos;,
      &apos;gender&apos; : &apos;Female&apos;,
      &apos;hiking&apos; : false,
      &apos;running&apos; : false,
      &apos;swimming&apos; : false
    })
  }

  // &#x63D0;&#x4EA4;&#x7684;&#x57F7;&#x884C;&#x7684; function
  submitForm(value: any): void {
    console.log(&apos;Reactive Form Data:&apos;, value);
  }
}
</code></pre>
<pre><code>//app.complexform.html

&lt;div class=&quot;jumbotron&quot;&gt;
    &lt;h2&gt;Data Driven (Reactive) Form&lt;/h2&gt;
    &lt;!-- &#x73FE;&#x5728;&#x6211;&#x5011;&#x4E0D;&#x5BA3;&#x544A;&#x5340;&#x57DF;&#x8B8A;&#x6578;&#x4E86;&#xFF0C;&#x6539;&#x7528;formGroup &#x9019;&#x500B;&#x6307;&#x4EE4;&#xFF0C;&#x4E26;&#x5C07;&#x5B83;&#x5B9A;&#x7FA9;&#x6210; complexForm &#x7269;&#x4EF6;&#x3002; complexForm &#x5C07;&#x6703;&#x63A7;&#x5236;&#x8868;&#x683C;&#x6240;&#x6709;&#x7684;&#x8B8A;&#x6578; --&gt;
    &lt;form [formGroup]=&quot;complexForm&quot; (ngSubmit)=&quot;submitForm(complexForm.value)&quot;&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;First Name:&lt;/label&gt;
        &lt;!-- &#x4E0D;&#x7528; ngModel &#x800C;&#x6539;&#x7528; formControl &#x6307;&#x4EE4;&#x53EF;&#x4EE5;&#x540C;&#x6B65; input &#x5230; complexForm &#x7269;&#x4EF6;&#x3002;&#x73FE;&#x5728;&#x4E5F;&#x4E0D;&#x9700;&#x8981; name &#x5C6C;&#x6027;&#x4E86;&#xFF0C;&#x4F46;&#x9084;&#x662F;&#x53EF;&#x4EE5;&#x9078;&#x64C7;&#x52A0;&#x5165; --&gt;
        &lt;input class=&quot;form-control&quot; type=&quot;text&quot; placeholder=&quot;John&quot; [formControl]=&quot;complexForm.controls[&apos;firstName&apos;]&quot;&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Last Name&lt;/label&gt;
        &lt;input class=&quot;form-control&quot; type=&quot;text&quot; placeholder=&quot;Doe&quot; [formControl]=&quot;complexForm.controls[&apos;lastName&apos;]&quot;&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Gender&lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Male&quot; [formControl]=&quot;complexForm.controls[&apos;gender&apos;]&quot;&gt;
          Male
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;!-- radio &#x548C; checkbox &#x7528;&#x6CD5;&#x4E5F;&#x4E00;&#x6A23; --&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Female&quot; [formControl]=&quot;complexForm.controls[&apos;gender&apos;]&quot;&gt;
          Female
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Activities&lt;/label&gt;
      &lt;/div&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;hiking&quot; name=&quot;hiking&quot; [formControl]=&quot;complexForm.controls[&apos;hiking&apos;]&quot;&gt; Hiking
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;swimming&quot; name=&quot;swimming&quot; [formControl]=&quot;complexForm.controls[&apos;swimming&apos;]&quot;&gt; Swimming
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;running&quot; name=&quot;running&quot; [formControl]=&quot;complexForm.controls[&apos;running&apos;]&quot;&gt; Running
      &lt;/label&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;button type=&quot;submit&quot; class=&quot;btn btn-default&quot;&gt;Submit&lt;/button&gt;
      &lt;/div&gt;
    &lt;/form&gt;
  &lt;/div&gt;
</code></pre>
<p>&#x4E0A;&#x9762;&#x8907;&#x96DC;&#x4E00;&#x9EDE;&#x9EDE;&#x7684;&#x7BC4;&#x4F8B;&#xFF0C;&#x66F4;&#x8CBC;&#x5207; Angular &#x7684;&#x7528;&#x6CD5;&#xFF0C;&#x8DD1;&#x51FA;&#x4F86;&#x6703;&#x9577;&#x9019;&#x6A23;&#x3002;<br>
&#x4E5F;&#x53EF;&#x4EE5;&#x770B;&#x5230; Female &#x70BA;&#x9810;&#x8A2D;&#x503C;&#x3002;<br>
<img src="https://cdn.scotch.io/4/72I21SlVSd6bOlWa8iIo_Screen%20Shot%202016-09-21%20at%203.36.31%20PM.png" alt></p>
<h2>&#x8868;&#x683C;&#x9A57;&#x8B49;</h2>
<p>Angular 2 &#x7684;&#x8868;&#x683C;&#x9A57;&#x8B49;&#x652F;&#x63F4;&#x6A21;&#x677F;&#x63A7;&#x5236;&#x4EE5;&#x53CA;&#x7D44;&#x4EF6;&#x63A7;&#x5236;&#xFF0C;&#x4F46;&#x662F;&#x900F;&#x904E;&#x7D44;&#x4EF6;&#x63A7;&#x5236;&#x5728;&#x8868;&#x683C;&#x9A57;&#x8B49;&#x4E0A;&#x6709;&#x66F4;&#x5927;&#x7684;&#x5F48;&#x6027;&#x3002;&#x8A73;&#x7D30;&#x53EF;&#x4EE5;&#x53C3;&#x8003; <a href="https://angular.io/docs/ts/latest/guide/forms.html" target="_blank">Angular 2 docs</a>&#x3002;</p>
<p>&#x6211;&#x5011;&#x5F9E;&#x8907;&#x96DC;&#x677F;&#x4F86;&#x52A0;&#x5165;&#x8868;&#x683C;&#x9A57;&#x8B49;&#x529F;&#x80FD;</p>
<pre><code>//app.validationform.ts

import { Component } from &apos;@angular/core&apos;;
// &#x5F15;&#x5165; Validators
import { FormGroup, FormBuilder, Validators } from &apos;@angular/forms&apos;;

@Component({
  selector: &apos;form-validation&apos;,
  template : &apos;app.validationform.html&apos;
})
export class FormValidationComponent {
  complexForm : FormGroup;

  constructor(fb: FormBuilder){
    this.complexForm = fb.group({
      // &#x8868;&#x793A;&#x4E00;&#x5B9A;&#x8981;&#x8F38;&#x5165;
      &apos;firstName&apos; : [null, Validators.required],
      // &#x8868;&#x793A;&#x4E00;&#x5B9A;&#x8981;&#x8F38;&#x5165;&#xFF0C;&#x800C;&#x4E14;&#x6700;&#x77ED;&#x70BA;5&#x500B;&#x5B57;&#x5143;&#xFF0C;&#x6700;&#x591A;&#x70BA;10&#x500B;&#x5B57;&#x5143;&#x3002;&#x6709;&#x591A;&#x500B;&#x898F;&#x5247;&#x6642;&#x7528;&#x9663;&#x5217;&#x5305;&#x4F4F;&#x3002;
      &apos;lastName&apos;: [null,  Validators.compose([Validators.required, Validators.minLength(5), Validators.maxLength(10)])],
      &apos;gender&apos; : [null, Validators.required],
      &apos;hiking&apos; : [false],
      &apos;running&apos; : [false],
      &apos;swimming&apos; : [false]
    })
    
    // &#x7528;&#x4F86;&#x89C0;&#x5BDF;&#x8868;&#x683C;&#x5143;&#x7D20;&#x7684;&#x8B8A;&#x5316;
    console.log(this.complexForm);
    this.complexForm.valueChanges.subscribe( (form: any) =&gt; {
      console.log(&apos;form changed to:&apos;, form);
    }
    );
  }

  // &#x63D0;&#x4EA4;&#x57F7;&#x884C;&#x7684;&#x7A0B;&#x5F0F;
  submitForm(value: any){
    console.log(value);
  }
}
</code></pre>
<pre><code>  //app.validationform.html
  
  &lt;div class=&quot;jumbotron&quot;&gt;
    &lt;h2&gt;Form with Validations&lt;/h2&gt;
    &lt;form [formGroup]=&quot;complexForm&quot; (ngSubmit)=&quot;submitForm(complexForm.value)&quot;&gt;
      &lt;!-- &#x586B;&#x5BEB;&#x7684;&#x503C;&#x5FC5;&#x9808;&#x6709;&#x6548; &#x4E14; &#x53EF;&#x4EE5;&#x8B93;&#x4F7F;&#x7528;&#x8005;&#x9EDE;&#x64CA;&#x904E;&#x4E00;&#x6B21;&#x4E4B;&#x5F8C;&#x624D;&#x6703;&#x986F;&#x793A; Error ( ngClass &#x4F7F;&#x984F;&#x8272;&#x6539;&#x8B8A;) --&gt;
      &lt;div class=&quot;form-group&quot; [ngClass]=&quot;{&apos;has-error&apos;:!complexForm.controls[&apos;firstName&apos;].valid &amp;&amp; complexForm.controls[&apos;firstName&apos;].touched}&quot;&gt;
        &lt;label&gt;First Name:&lt;/label&gt;
        &lt;input class=&quot;form-control&quot; type=&quot;text&quot; placeholder=&quot;John&quot; [formControl]=&quot;complexForm.controls[&apos;firstName&apos;]&quot;&gt;
        &lt;!-- .hasError(&apos;why&apos;)&#x53EF;&#x4EE5;&#x5728;&#x767C;&#x751F;&#x586B;&#x5BEB;&#x932F;&#x8AA4;&#x6642;&#x544A;&#x8A34;&#x4F7F;&#x7528;&#x8005;&#x70BA;&#x751A;&#x9EBC; Error --&gt;
        &lt;div *ngIf=&quot;complexForm.controls[&apos;firstName&apos;].hasError(&apos;required&apos;) &amp;&amp; complexForm.controls[&apos;firstName&apos;].touched&quot; class=&quot;alert alert-danger&quot;&gt;You must include a first name.&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot; [ngClass]=&quot;{&apos;has-error&apos;:!complexForm.controls[&apos;lastName&apos;].valid &amp;&amp; complexForm.controls[&apos;lastName&apos;].touched}&quot;&gt;
        &lt;label&gt;Last Name&lt;/label&gt;
        &lt;input class=&quot;form-control&quot; type=&quot;text&quot; placeholder=&quot;Doe&quot; [formControl]=&quot;complexForm.controls[&apos;lastName&apos;]&quot;&gt;
        &lt;!-- .hasError(&apos;required&apos;)&#x4EE3;&#x8868;&#x5FC5;&#x9808;&#x8981;&#x586B; --&gt;
        &lt;div *ngIf=&quot;complexForm.controls[&apos;lastName&apos;].hasError(&apos;required&apos;) &amp;&amp; complexForm.controls[&apos;lastName&apos;].touched&quot; class=&quot;alert alert-danger&quot;&gt;You must include a last name.&lt;/div&gt;
        &lt;!-- .hasError(&apos;minlength&apos;)&#x4EE3;&#x8868;&#x592A;&#x77ED; --&gt;
        &lt;div *ngIf=&quot;complexForm.controls[&apos;lastName&apos;].hasError(&apos;minlength&apos;) &amp;&amp; complexForm.controls[&apos;lastName&apos;].touched&quot; class=&quot;alert alert-danger&quot;&gt;Your last name must be at least 5 characters long.&lt;/div&gt;
        &lt;div *ngIf=&quot;complexForm.controls[&apos;lastName&apos;].hasError(&apos;maxlength&apos;) &amp;&amp; complexForm.controls[&apos;lastName&apos;].touched&quot; class=&quot;alert alert-danger&quot;&gt;Your last name cannot exceed 10 characters.&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Gender&lt;/label&gt;
        &lt;!-- Radio &#x7121;&#x6CD5;&#x4E0A;&#x8272;&#xFF0C;&#x6240;&#x4EE5;&#x53EA;&#x7528;&#x63D0;&#x793A;&#x5B57;&#x4E32; --&gt;
        &lt;div class=&quot;alert alert-danger&quot; *ngIf=&quot;!complexForm.controls[&apos;gender&apos;].valid &amp;&amp; complexForm.controls[&apos;gender&apos;].touched&quot;&gt;You must select a gender.&lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Male&quot; [formControl]=&quot;complexForm.controls[&apos;gender&apos;]&quot;&gt;
          Male
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;radio&quot;&gt;
        &lt;label&gt;
          &lt;input type=&quot;radio&quot; name=&quot;gender&quot; value=&quot;Female&quot; [formControl]=&quot;complexForm.controls[&apos;gender&apos;]&quot;&gt;
          Female
        &lt;/label&gt;
      &lt;/div&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;label&gt;Activities&lt;/label&gt;
      &lt;/div&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;hiking&quot; name=&quot;hiking&quot; [formControl]=&quot;complexForm.controls[&apos;hiking&apos;]&quot;&gt; Hiking
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;swimming&quot; name=&quot;swimming&quot; [formControl]=&quot;complexForm.controls[&apos;swimming&apos;]&quot;&gt; Swimming
      &lt;/label&gt;
      &lt;label class=&quot;checkbox-inline&quot;&gt;
        &lt;input type=&quot;checkbox&quot; value=&quot;running&quot; name=&quot;running&quot; [formControl]=&quot;complexForm.controls[&apos;running&apos;]&quot;&gt; Running
      &lt;/label&gt;
      &lt;div class=&quot;form-group&quot;&gt;
        &lt;button type=&quot;submit&quot; class=&quot;btn btn-primary&quot; [disabled]=&quot;!complexForm.valid&quot;&gt;Submit&lt;/button&gt;
      &lt;/div&gt;
    &lt;/form&gt;
  &lt;/div&gt;
</code></pre>
<p><img src="https://cdn.scotch.io/4/tjy7UEFCSMyEfV41mSAn_form-validation.gif" alt></p>
 <br>
                                                    </div>
                    </div>
                
