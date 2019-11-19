---
title: Angular 2 單元測試 Unit Test
date: 2017-01-14 23:44:43
tags: [Angular2, Angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x7576;&#x6211;&#x5011;&#x628A;&#x7A0B;&#x5F0F;&#x5BEB;&#x5B8C;&#x4E4B;&#x5F8C;&#xFF0C;&#x901A;&#x5E38;&#x6703;&#x9700;&#x8981;&#x505A;&#x6E2C;&#x8A66;&#xFF0C;&#x53EF;&#x80FD;&#x5C31;&#x662F;&#x8DD1;&#x8DD1;&#x770B;&#x770B;&#x6771;&#x897F;&#x6709;&#x6C92;&#x6709;&#x51FA;&#x4F86;&#x3001;&#x7B26;&#x5408;&#x9810;&#x671F;&#xFF0C;&#x6216;&#x8457;&#x5370;&#x51FA;&#x5167;&#x5BB9;&#x6216;&#x662F; log &#x4E0B;&#x4F86;&#x3002;&#x6BCF;&#x6B21;&#x90FD;&#x8981;&#x624B;&#x52D5;&#x6E2C;&#x8A66;&#x5F88;&#x9EBB;&#x7169;&#xFF0C;&#x6709;&#x6642;&#x5019;&#x4E5F;&#x6703;&#x6709;&#x6B7B;&#x89D2;&#xFF0C;&#x751A;&#x81F3;&#x7576;&#x6D41;&#x7A0B;&#x7E41;&#x96DC;&#x6642;&#xFF0C;&#x624B;&#x52D5;&#x6E2C;&#x8A66;&#x7D55;&#x5C0D;&#x4E0D;&#x662F;&#x500B;&#x597D;&#x9078;&#x64C7;&#xFF0C;&#x9019;&#x6642;&#x5019;&#x5C31;&#x6703;&#x7528;&#x5230;&#x55AE;&#x5143;&#x6E2C;&#x8A66; (Unit Test)&#x3002;</p>
<blockquote>
<p>&#x85C9;&#x7531;&#x5EFA;&#x7ACB;&#x53CA;&#x57F7;&#x884C;&#x55AE;&#x5143;&#x6E2C;&#x8A66;&#xFF0C;&#x6AA2;&#x67E5;&#x60A8;&#x7684;&#x7A0B;&#x5F0F;&#x78BC;&#x662F;&#x5426;&#x5982;&#x9810;&#x671F;&#x822C;&#x57F7;&#x884C;&#x3002; &#x9019;&#x4E4B;&#x6240;&#x4EE5;&#x7A31;&#x70BA;&#x55AE;&#x5143;&#x6E2C;&#x8A66;&#xFF0C;&#x662F;&#x56E0;&#x70BA;&#x60A8;&#x5C07;&#x7A0B;&#x5F0F;&#x529F;&#x80FD;&#x5206;&#x89E3;&#x6210;&#x96E2;&#x6563;&#x7684;&#x53EF;&#x6E2C;&#x8A66;&#x884C;&#x70BA;&#xFF0C;&#x9019;&#x4E9B;&#x884C;&#x70BA;&#x80FD;&#x505A;&#x70BA;&#x500B;&#x5225;&#x7684;&#x300C;&#x55AE;&#x4F4D;&#x300D;(unit) &#x52A0;&#x4EE5;&#x6E2C;&#x8A66;&#x3002;</p>
</blockquote>
<p>&#x60F3;&#x66F4;&#x4E86;&#x89E3;&#x55AE;&#x5143;&#x6E2C;&#x8A66;&#x53EF;&#x4EE5;&#x770B;<a href="https://www.codedata.com.tw/java/unit-test-the-way-changes-my-programming" target="_blank">&#x9019;&#x7BC7;</a></p>
<h2>&#x6E2C;&#x8A66;&#x74B0;&#x5883;</h2>
<h3>&#x6982;&#x5FF5;</h3>
<p>&#x9019;&#x908A;&#x7528; Jasmine &#x6E2C;&#x8A66;&#xFF0C;&#x4F46;&#x5176;&#x5BE6;&#x4E5F;&#x53EF;&#x4EE5;&#x7528;&#x5176;&#x4ED6;&#x7684;&#x6E2C;&#x8A66;&#x6846;&#x67B6;&#x50CF;&#x662F; <a href="https://mochajs.org/" target="_blank">Mocha</a>.</p>
<p>&#x6E2C;&#x8A66;&#x89C0;&#x5FF5;&#xFF1A;</p>
<ul>
<li>Suites&#x200A;&#x2014;&#x200A;<code>describe(string, function)</code> &#x51FD;&#x6578;&#xFF0C;&#x4E0B;&#x6A19;&#x984C;&#x7136;&#x5F8C;&#x5305;&#x542B;&#x591A;&#x500B; <code>Specs</code>&#x3002;</li>
<li>Specs&#x200A;&#x2014;&#x200A;<code>it(string, function)</code> &#x51FD;&#x6578;&#xFF0C;&#x4E0B;&#x6A19;&#x984C;&#x7136;&#x5F8C;&#x5305;&#x542B;&#x591A;&#x500B; <code>expectations</code>.</li>
<li>Expectations&#x200A;&#x2014;&#x200A;&#x9810;&#x671F;&#x6703;&#x767C;&#x751F;&#x7684;&#x7D50;&#x679C;&#xFF0C;&#x8A9E;&#x6CD5;&#x50CF;&#x662F; <code>expect(actual).toBe(expected)</code>&#x3002;</li>
<li>Matchers&#x200A;&#x2014;&#x200A;&#x5224;&#x65B7;&#x662F;&#x5426;&#x7B26;&#x5408;&#x9810;&#x671F;&#x3002;&#x50CF;&#x662F;&#xFF1A; <code>toBe(expected)</code>&#x3001;<code>toEqual(expected)</code>&#x3002;</li>
</ul>
<h3>Setup</h3>
<p>&#x4F60;&#x53EF;&#x4EE5;&#x7528; Jasmine &#x7684; SpecRunner.html&#xFF0C;&#x6216;&#x662F;&#x63A1;&#x7528;&#x6E2C;&#x8A66;&#x904B;&#x884C;&#x6846;&#x67B6;&#x50CF;&#x662F; Karma&#x3002;<br>
&#x901A;&#x5E38;&#x958B;&#x767C; Angular &#x7528;&#x7684;&#x5927;&#x578B;&#x5957;&#x4EF6; (Angular CLI, Angular Seed) &#x5C31;&#x6703;&#x5305;&#x542B;&#x55AE;&#x5143;&#x6E2C;&#x8A66;&#x7684;&#x6A94;&#x6848;&#x4E86;&#x3002;</p>
<p>Plunker &#x7528;&#x7684;&#x6E2C;&#x8A66;&#x74B0;&#x5883;&#xFF1A;</p>
<pre><code>&lt;!-- Jasmine dependencies --&gt;
&lt;link href=&quot;https://cdnjs.cloudflare.com/ajax/libs/jasmine/2.4.1/jasmine.css&quot; /&gt;
&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/jasmine/2.4.1/jasmine.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/jasmine/2.4.1/jasmine-html.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/jasmine/2.4.1/boot.js&quot;&gt;&lt;/script&gt;

&lt;!-- Angular 2 dependencies --&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/zone.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/long-stack-trace-zone.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/reflect-metadata@0.1.3/Reflect.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/systemjs@0.19.31/dist/system.js&quot;&gt;&lt;/script&gt;

&lt;!-- Angular 2 testing dependencies --&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/proxy.js?main=browser&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/sync-test.js?main=browser&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/jasmine-patch.js?main=browser&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/zone.js@0.6.25/dist/async-test.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://unpkg.com/zone.js/dist/fake-async-test.js?main=browser&quot;&gt;&lt;/script&gt;

&lt;script src=&quot;config.js&quot;&gt;&lt;/script&gt;
&lt;script&gt;
  //load all dependencies at the same time
  Promise.all([
    //required to test on browser
    System.import(&apos;src/setup.spec&apos;),
    //specs
    System.import(&apos;src/languagesService.spec&apos;),
    ...
  ]).then(function(modules) {
    //manually trigger Jasmine test-runner
    window.onload();
  }).catch(console.error.bind(console));
&lt;/script&gt;
</code></pre>
<p><a href="https://embed.plnkr.co/jm6T17qPbzM8abmRMckw/" target="_blank">&#x9019;&#x908A;</a>&#x53EF;&#x4EE5;&#x770B; Plunker &#x5BE6;&#x969B;&#x57F7;&#x884C;&#x6E2C;&#x8A66;&#x7684;&#x6A23;&#x5B50;&#x3002;</p>
<h2>&#x7BC4;&#x4F8B;</h2>
<p>&#x6E2C;&#x8A66;&#x7BC4;&#x4F8B;&#x4F86;&#x81EA;<a href="https://medium.com/google-developer-experts/angular-2-testing-guide-a485b6cb1ef0#.t7mwszbtm" target="_blank">&#x9019;&#x908A;</a></p>
<h3>&#x6E2C;&#x8A66; DI</h3>
<p><code>TestBed</code> &#x5982;&#x540C; <code>@NgModule</code> &#x5E6B;&#x52A9;&#x6211;&#x5011;&#x5EFA;&#x7ACB;&#x6CE8;&#x5165;&#x4F9D;&#x8CF4; (DI) &#x7684;&#x55AE;&#x5143;&#x6E2C;&#x8A66;. &#x547C;&#x53EB; <code>TestBed.configureTestingModule</code> &#x4F86;&#x57F7;&#x884C;&#x3002;</p>
<pre><code>@NgModule({
  declarations: [ ComponentToTest ] 
  providers: [ MyService ]
}) 
class AppModule { }
TestBed.configureTestingModule({
  declarations: [ ComponentToTest ],
  providers: [ MyService ]  
});
//&#x5F9E; TestBed &#x53D6;&#x5F97;&#x5BE6;&#x4F8B; (root injector)
let service = TestBed.get(MyService);
</code></pre>
<p><code>inject</code> &#x8B93;&#x6211;&#x5011;&#x5728; TestBed &#x5C64;&#x7D1A;&#x53D6;&#x5F97;&#x4F9D;&#x8CF4;</p>
<pre><code>it(&apos;should return ...&apos;, inject([MyService], service =&gt; { 
  service.foo();
}));
</code></pre>
<p>Component <code>injector</code> &#x8B93;&#x6211;&#x5011;&#x5728; Component &#x5C64;&#x7D1A;&#x53D6;&#x5F97;&#x4F9D;&#x8CF4;&#x3002;</p>
<pre><code>@Component({ 
  providers: [ MyService ] 
}) 
class ComponentToTest { }
let fixture = TestBed.createComponent(ComponentToTest);
let service = fixture.debugElement.injector.get(MyService);
</code></pre>
<p>&#x751A;&#x9EBC;&#x5C64;&#x7D1A;&#x7684;&#x4F9D;&#x8CF4;&#x53D6;&#x6C7A;&#x65BC;&#x7576;&#x521D;&#x5B9A;&#x7FA9;&#x3002;Component &#x5C64;&#x7D1A;&#x5C31;&#x7121;&#x6CD5;&#x4F7F;&#x7528; <code>TestBed.get</code> &#x6216; <code>inject</code>&#x3002;</p>
<p>&#x9996;&#x5148;&#x6211;&#x5011;&#x7528; TestBed &#x7684; <code>TestBed.configureTestingModule</code> &#x8F09;&#x5165;&#x4F9D;&#x8CF4;&#x7684;&#x4F86;&#x6E90;&#x3002;&#x63A5;&#x8457;&#x7528; <code>inject</code> &#x53BB;&#x81EA;&#x52D5;&#x5BE6;&#x9AD4;&#x5316;&#x4F9D;&#x8CF4;&#x3002;</p>
<pre><code>describe(&apos;Service: LanguagesService&apos;, () =&gt; {
  let service;

  beforeEach(() =&gt; TestBed.configureTestingModule({
    providers: [ LanguagesService ]
  }));

  beforeEach(inject([LanguagesService], s =&gt; {
    service = s;
  }));

  it(&apos;should return available languages&apos;, () =&gt; {
    expect(service.get()).toContain(&apos;en&apos;);
  });
});
</code></pre>
<h3>&#x540C;&#x6B65;&#x7570;&#x6B65;</h3>
<p>&#x540C;&#x6B65;</p>
<pre><code>// synchronous
  beforeEach(() =&gt; {
    fixture = TestBed.createComponent(MyTestComponent);
  });
</code></pre>
<p>&#x7570;&#x6B65;</p>
<pre><code>// asynchronous 
  beforeEach(async(() =&gt; {
    TestBed.configureTestingModule({
      declarations: [ MyTestComponent ],
    }).compileComponents(); // compile external templates and css
  }));
</code></pre>
<h3>&#x6E2C;&#x8A66;&#x7D44;&#x4EF6;</h3>
<pre><code>
// Usage:    &lt;greeter name=&quot;Joe&quot;&gt;&lt;/greeter&gt; 
// Renders:  &lt;h1&gt;Hello Joe!&lt;/h1&gt;
@Component({
  selector: &apos;greeter&apos;,
  template: `&lt;h1&gt;Hello {{name}}!&lt;/h1&gt;`
})
export class Greeter { 
  @Input() name;
}
</code></pre>
<pre><code>
describe(&apos;Component: Greeter&apos;, () =&gt; {
  let fixture, greeter, element, de;
  
  //setup
  beforeEach(() =&gt; {
    TestBed.configureTestingModule({
      declarations: [ Greeter ]
    });

    fixture = TestBed.createComponent(Greeter);
    greeter = fixture.componentInstance;  // to access properties and methods
    element = fixture.nativeElement;      // to access DOM element
    de = fixture.debugElement;            // test helper
  });
  
  //specs
  it(&apos;should render `Hello World!`&apos;, async(() =&gt; {
    greeter.name = &apos;World&apos;;
    //trigger change detection
    fixture.detectChanges();
    fixture.whenStable().then(() =&gt; { 
      expect(element.querySelector(&apos;h1&apos;).innerText).toBe(&apos;Hello World!&apos;);
      expect(de.query(By.css(&apos;h1&apos;)).nativeElement.innerText).toBe(&apos;Hello World!&apos;);
    });
  }));
}) 
</code></pre>
<h3>&#x6E2C;&#x8A66;&#x670D;&#x52D9; (Service)</h3>
<pre><code>//a simple service
export class LanguagesService {
  get() {
    return [&apos;en&apos;, &apos;es&apos;, &apos;fr&apos;];
  }
}
</code></pre>
<pre><code>describe(&apos;Service: LanguagesService&apos;, () =&gt; {
  let service;

  beforeEach(() =&gt; TestBed.configureTestingModule({
    providers: [ LanguagesService ]
  }));

  beforeEach(inject([LanguagesService], s =&gt; {
    service = s;
  }));

  it(&apos;should return available languages&apos;, () =&gt; {
    let languages = service.get();
    expect(languages).toContain(&apos;en&apos;);
    expect(languages).toContain(&apos;es&apos;);
    expect(languages).toContain(&apos;fr&apos;);
    expect(languages.length).toEqual(3);
  });
});
</code></pre>
<h3>&#x6E2C;&#x8A66; HTTP</h3>
<pre><code>export class LanguagesServiceHttp {
  constructor(private http:Http) { }
  
  get(){
    return this.http.get(&apos;api/languages.json&apos;)
      .map(response =&gt; response.json());
  }
}
</code></pre>
<pre><code>describe(&apos;Service: LanguagesServiceHttp&apos;, () =&gt; {
  let service;
  
  //setup
  beforeEach(() =&gt; TestBed.configureTestingModule({
    imports: [ HttpModule ],
    providers: [ LanguagesServiceHttp ]
  }));
  
  beforeEach(inject([LanguagesServiceHttp], s =&gt; {
    service = s;
  }));
  
  //specs
  it(&apos;should return available languages&apos;, async(() =&gt; {
    service.get().subscribe(x =&gt; { 
      expect(x).toContain(&apos;en&apos;);
      expect(x).toContain(&apos;es&apos;);
      expect(x).toContain(&apos;fr&apos;);
      expect(x.length).toEqual(3);
    });
  }));
}) 
</code></pre>
<h3>MockBackend</h3>
<p>&#x66F4;&#x63A5;&#x8FD1; HTTP &#x908F;&#x8F2F;&#x7684;&#x6E2C;&#x8A66;</p>
<pre><code>describe(&apos;MockBackend: LanguagesServiceHttp&apos;, () =&gt; {
  let mockbackend, service;

  //setup
  beforeEach(() =&gt; {
    TestBed.configureTestingModule({
      imports: [ HttpModule ],
      providers: [
        LanguagesServiceHttp,
        { provide: XHRBackend, useClass: MockBackend }
      ]
    })
  });
    
  beforeEach(inject([LanguagesServiceHttp, XHRBackend], (_service, _mockbackend) =&gt; {
    service = _service;
    mockbackend = _mockbackend;
  }));

  //specs
  it(&apos;should return mocked response (async)&apos;, async(() =&gt; {
    let response = [&quot;ru&quot;, &quot;es&quot;];
    mockbackend.connections.subscribe(connection =&gt; {
      connection.mockRespond(new Response({body: JSON.stringify(response)}));
    });
    service.get().subscribe(languages =&gt; {
      expect(languages).toContain(&apos;ru&apos;);
      expect(languages).toContain(&apos;es&apos;);
      expect(languages.length).toBe(2);
    });
  }));  
})
</code></pre>
<h3>&#x6E2C;&#x8A66;&#x6307;&#x4EE4;(Directive)</h3>
<pre><code>// Example: &lt;div log-clicks&gt;&lt;/div&gt;
@Directive({
  selector: &quot;[log-clicks]&quot;
})
export class logClicks {
  counter = 0;
  @Output() changes = new EventEmitter();
  
  @HostListener(&apos;click&apos;, [&apos;$event.target&apos;])
  clicked(target) { 
    console.log(`Click on [${target}]: ${++this.counter}`);
    //we use emit as next is marked as deprecated
    this.changes.emit(this.counter);
  }
}
</code></pre>
<p>&#x6211;&#x5011;&#x5EFA;&#x69CB;&#x4E00;&#x500B;&#x8DDF;&#x8981;&#x6E2C;&#x8A66;&#x7684;&#x7D44;&#x4EF6;&#x5F88;&#x50CF;&#x7684;&#x7D44;&#x4EF6; Container &#xFF0C;&#x62FF;&#x4F86;&#x505A;&#x6E2C;&#x8A66;</p>
<pre><code>@Component({ 
  selector: &apos;container&apos;,
  template: `&lt;div log-clicks (changes)=&quot;changed($event)&quot;&gt;&lt;/div&gt;`,
  directives: [logClicks]
})
export class Container {  
  @Output() changes = new EventEmitter();
  
  changed(value){
    this.changes.emit(value);
  }
}

describe(&apos;Directive: logClicks&apos;, () =&gt; {
  let fixture;
  let container;
  let element;  

  //setup
  beforeEach(() =&gt; {
    TestBed.configureTestingModule({
      declarations: [ Container, logClicks ]
    });

    fixture = TestBed.createComponent(Container);
    container = fixture.componentInstance; // to access properties and methods
    element = fixture.nativeElement;       // to access DOM element
  });
  
  //specs
  it(&apos;should increment counter&apos;, fakeAsync(() =&gt; {
    let div = element.querySelector(&apos;div&apos;);
    //set up subscriber
    container.changes.subscribe(x =&gt; { 
      expect(x).toBe(1);
    });
    //trigger click on container
    div.click();
    //execute all pending asynchronous calls
    tick();
  }));
}) 
</code></pre>
<h3>&#x6E2C;&#x8A66; Pipe</h3>
<pre><code>import {Pipe, PipeTransform} from &apos;@angular/core&apos;;
@Pipe({
  name: &apos;capitalise&apos;
})
export class CapitalisePipe implements PipeTransform {
  transform(value: string): string {
    if (typeof value !== &apos;string&apos;) {
      throw new Error(&apos;Requires a String as input&apos;);
    }
    return value.toUpperCase();
  }
}
</code></pre>
<pre><code>describe(&apos;Pipe: CapitalisePipe&apos;, () =&gt; {
  let pipe;
  
  //setup
  beforeEach(() =&gt; TestBed.configureTestingModule({
    providers: [ CapitalisePipe ]
  }));
  
  beforeEach(inject([CapitalisePipe], p =&gt; {
    pipe = p;
  }));
  
  //specs
  it(&apos;should work with empty string&apos;, () =&gt; {
    expect(pipe.transform(&apos;&apos;)).toEqual(&apos;&apos;);
  });
  
  it(&apos;should capitalise&apos;, () =&gt; {
    expect(pipe.transform(&apos;wow&apos;)).toEqual(&apos;WOW&apos;);
  });
  
  it(&apos;should throw with invalid values&apos;, () =&gt; {
    //must use arrow function for expect to capture exception
    expect(()=&gt;pipe.transform(undefined)).toThrow();
    expect(()=&gt;pipe.transform()).toThrow();
    expect(()=&gt;pipe.transform()).toThrowError(&apos;Requires a String as input&apos;);
  });
}) 
</code></pre>
<h3>&#x6E2C;&#x8A66; Route</h3>
<pre><code>@Component({
  selector: &apos;my-app&apos;,
  template: `&lt;router-outlet&gt;&lt;/router-outlet&gt;`
})
class TestComponent { }

@Component({
  selector: &apos;home&apos;,
  template: `&lt;h1&gt;Home&lt;/h1&gt;`
})
export class Home { }

export const routes: Routes = [
  { path: &apos;&apos;, redirectTo: &apos;home&apos;, pathMatch: &apos;full&apos; },
  { path: &apos;home&apos;, component: Home },
  { path: &apos;**&apos;, redirectTo: &apos;home&apos; }
];

@NgModule({
  imports: [
    BrowserModule, RouterModule.forRoot(routes),
  ],
  declarations: [TestComponent, Home],
  bootstrap: [TestComponent],
  exports: [TestComponent] 
})
export class AppModule {}
</code></pre>
<pre><code>describe(&apos;Router tests&apos;, () =&gt; {
  //setup
  beforeEach(() =&gt; {
    TestBed.configureTestingModule({
      imports: [
        RouterTestingModule.withRoutes(routes),
        AppModule
      ]
    });
  });
  
  //specs
  it(&apos;can navigate to home (async)&apos;, async(() =&gt; {
    let fixture = TestBed.createComponent(TestComponent);
    TestBed.get(Router)
      .navigate([&apos;/home&apos;])
        .then(() =&gt; {
          expect(location.pathname.endsWith(&apos;/home&apos;)).toBe(true);
        }).catch(e =&gt; console.log(e));
  }));
  
  it(&apos;can navigate to home (fakeAsync/tick)&apos;, fakeAsync(() =&gt; {
    let fixture = TestBed.createComponent(TestComponent);
    TestBed.get(Router).navigate([&apos;/home&apos;]);
    fixture.detectChanges();
    //execute all pending asynchronous calls
    tick();    
    expect(location.pathname.endsWith(&apos;/home&apos;)).toBe(true);
  }));
  
  it(&apos;can navigate to home (done)&apos;, done =&gt; {
    let fixture = TestBed.createComponent(TestComponent);
    TestBed.get(Router)
      .navigate([&apos;/home&apos;])
        .then(() =&gt; {
          expect(location.pathname.endsWith(&apos;/home&apos;)).toBe(true);
          done();
        }).catch(e =&gt; console.log(e));
  });
});
</code></pre>
<h3>&#x6E2C;&#x8A66; EventEmitters</h3>
<pre><code>@Component({
  selector: &apos;counter&apos;,
  template: `
    &lt;div&gt;
      &lt;h1&gt;{{counter}}&lt;/h1&gt;
      &lt;button (click)=&quot;change(1)&quot;&gt;+1&lt;/button&gt;
      &lt;button (click)=&quot;change(-1)&quot;&gt;-1&lt;/button&gt;
    &lt;/div&gt;`
})
export class Counter {
  @Output() changes = new EventEmitter();
  
  constructor(){
    this.counter = 0;
  }
  
  change(increment) {
    this.counter += increment;
    //we use emit as next is marked as deprecated
    this.changes.emit(this.counter);
  }
}
</code></pre>
<pre><code>describe(&apos;EventEmitter: Counter&apos;, () =&gt; {
  let counter;
  
  //setup
  beforeEach(() =&gt; TestBed.configureTestingModule({
    providers: [ Counter ]
  }));
  
  beforeEach(inject([Counter], c =&gt; {
    counter = c;
  }))
  
  //specs
  it(&apos;should increment +1 (async)&apos;, async(() =&gt; {
    counter.changes.subscribe(x =&gt; { 
      expect(x).toBe(1);
    });
    counter.change(1);
  }));

  it(&apos;should decrement -1 (async)&apos;, async(() =&gt; {
    counter.changes.subscribe(x =&gt; { 
      expect(x).toBe(-1);
    });
    counter.change(-1);
  }));
}) 
</code></pre>
 <br>
                                                    </div>
                    </div>
                
