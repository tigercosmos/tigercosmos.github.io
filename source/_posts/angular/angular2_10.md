---
title: Angular 2 HTTP 方法－－讓我 Call API
date: 2016-12-26 23:52:38
tags: [angular2, angular, 鐵人賽, Angular 2 之 30 天邁向神乎其技之路]
---
<h2>&#x524D;&#x8A00;</h2>
<p>&#x7DB2;&#x7AD9;&#x6709;&#x4E86;&#x4E00;&#x5806;&#x7684;&#x5143;&#x7D20;&#x3001;&#x52D5;&#x756B;&#x3001;&#x5716;&#x7247;&#x3001;&#x6587;&#x5B57;&#xFF0C;&#x53EF;&#x80FD;&#x770B;&#x8D77;&#x4F86;&#x5F88;&#x70AB;&#x5F88;&#x53B2;&#x5BB3;&#xFF0C;&#x4F46;&#x662F;&#x9019;&#x6A23;&#x5C31;&#x53EA;&#x80FD;&#x662F;&#x975C;&#x614B;&#x7684;&#x7DB2;&#x7AD9;&#xFF0C;&#x60F3;&#x8981;&#x5BE6;&#x73FE;&#x8CFC;&#x7269;&#x8ECA;&#x3001;&#x6703;&#x54E1;&#x6A5F;&#x5236;&#x3001;&#x7559;&#x8A00;&#x677F;&#x3001;&#x8A0E;&#x8AD6;&#x5340;&#x3001;&#x6295;&#x7968;&#x5340;&#x3001;&#x8A0A;&#x606F;&#x767C;&#x4F48;&#x3001;&#x5546;&#x54C1;&#x767C;&#x4F48;&#x7B49;&#x7B49;&#x529F;&#x80FD;&#xFF0C;&#x9032;&#x800C;&#x8A2D;&#x8A08;&#x51FA;&#x53EF;&#x8207;&#x7DB2;&#x53CB;&#x9032;&#x884C;&#x4E92;&#x52D5;&#x7684;&#x529F;&#x80FD;&#x3002;&#x800C;&#x8981;&#x5BE6;&#x73FE;&#x9019;&#x4E9B;&#x529F;&#x80FD;&#xFF0C;&#x4E0D;&#x5916;&#x4E4E;&#x5C31;&#x662F;&#x4E00;&#x76F4;&#x547C;&#x53EB; API&#xFF0C;&#x7136;&#x5F8C;&#x900F;&#x904E;&#x5F8C;&#x7AEF;&#x548C;&#x8CC7;&#x6599;&#x5EAB;&#x7684;&#x8655;&#x7406;&#xFF0C;&#x518D;&#x5C07;&#x8CC7;&#x6599;&#x50B3;&#x56DE;&#x7D66;&#x7DB2;&#x7AD9;&#x3002;<br>
&#x524D;&#x7AEF;&#x548C;&#x5F8C;&#x7AEF;&#x7684;&#x9023;&#x7D50;&#xFF0C;&#x5C31;&#x662F;&#x900F;&#x904E; Http &#x65B9;&#x6CD5;&#xFF0C;&#x5305;&#x542B; get&#x3001;post&#x3001;head&#x3001;put&#x3001;patch &#x548C; delete&#x3002;&#x63A5;&#x4E0B;&#x4F86;&#x5C31;&#x4F86;&#x8AAA;&#x660E;&#x5982;&#x4F55;&#x5728; Angular 2 &#x4E2D;&#x5BE6;&#x73FE; HTTP &#x65B9;&#x6CD5;&#x3002;</p>
<h2>RxJS</h2>
<p>RxJS&#x662F;&#x4E00;&#x500B;&#x7B2C;&#x4E09;&#x65B9;&#x51FD;&#x5F0F;&#x5EAB;&#xFF0C;&#x7531; Angular &#x8D0A;&#x52A9;&#xFF0C;&#x5BE6;&#x73FE;&#x7570;&#x6B65;&#x89C0;&#x5BDF;&#x6A21;&#x5F0F;&#x3002;Angular &#x9ED8;&#x8A8D;&#x5C31;&#x6709;&#x5B89;&#x88DD; RxJS&#xFF0C;&#x56E0;&#x70BA; Observable &#x6A21;&#x5F0F;&#x88AB;&#x5EE3;&#x6CDB;&#x5728;&#x61C9;&#x7528;&#x5728; Angular &#x7A0B;&#x5E8F;&#x3002;Observable &#x662F;&#x4E00;&#x7A2E;&#x8DA8;&#x52E2;&#x3002;HTTP &#x5BA2;&#x6236;&#x7AEF;&#x5C31;&#x9700;&#x8981; RxJS&#xFF0C;&#x6240;&#x4EE5;&#x6211;&#x5011;&#x5FC5;&#x9808;&#x63A1;&#x7528;&#x984D;&#x5916;&#x7684;&#x6B65;&#x9A5F;&#x958B;&#x555F; RxJS Observables&#x3002;<br>
&#x4E8B;&#x5BE6;&#x4E0A;&#x53EF;&#x4EE5;&#x53EA;&#x8F09;&#x5165;&#x9700;&#x8981;&#x7684;&#x90E8;&#x5206;&#xFF0C;&#x4E0D;&#x904E;&#x5148;&#x5168;&#x5F15;&#x5165;&#x5427;&#xFF01;<br>
import <code>rxjs-operator</code> into <code>app.component.ts</code></p>
<pre><code>// Add all operators to Observable
import &apos;rxjs/Rx&apos;;
</code></pre>
<h2>HTTP &#x670D;&#x52D9;</h2>
<p>Angular Http client (&#x5BA2;&#x6236;&#x7AEF;) &#x548C;&#x4F3A;&#x670D;&#x5668;&#x901A;&#x8A0A;&#x662F;&#x85C9;&#x7531;&#x719F;&#x7FD2;&#x7684; Http &#x8981;&#x6C42;/&#x56DE;&#x61C9; (request/response) &#x5354;&#x8B70;&#x3002;&#x800C;&#x4E14; <code>Http</code> client &#x61C9;&#x8A72;&#x662F; Angular &#x4E2D;&#x95DC;&#x65BC; Http &#x6700;&#x5E38;&#x7528;&#x5230;&#x7684;&#x51FD;&#x5F0F;&#x5EAB;&#x4E86;&#x3002;</p>
<blockquote>
<p>&#x4F7F;&#x7528; Http client &#x7684;&#x6642;&#x5019;&#xFF0C;&#x61C9;&#x8A72;&#x5C07;&#x5C07;&#x670D;&#x52D9;&#x8A3B;&#x518A;&#x70BA;&#x4F9D;&#x8CF4;&#x6CE8;&#x5165;&#x7CFB;&#x7D71;&#x4E2D;&#x3002;</p>
</blockquote>
<p>&#x76F4;&#x63A5;&#x770B;&#x7BC4;&#x4F8B;</p>
<h3>GET</h3>
<pre><code>import { Injectable }     from &apos;@angular/core&apos;;
import { Http, Response } from &apos;@angular/http&apos;;
import { Observable }     from &apos;rxjs/Observable&apos;;
@Injectable()
export class HttpClientService {
  constructor (private http: Http) {}
  get(url: string, optionHeader?: {[header: string]: string}): Observable&lt;Response&gt; {
    let headers = new Headers();
    // set option header
    for(let header in optionHeader) {
      let value = optionHeader[header];
      headers.append(header, value);
    }
    return this.http.get(url, {headers: headers,})
                    .map(this.extractData)
                    .catch(this.handleError);
  }
  private extractData(res: Response) {
    let body = res.json();
    return body.data || { };
  }
  private handleError (error: Response | any) {
    // In a real world app, we might use a remote logging infrastructure
    let errMsg: string;
    if (error instanceof Response) {
      const body = error.json() || &apos;&apos;;
      const err = body.error || JSON.stringify(body);
      errMsg = `${error.status} - ${error.statusText || &apos;&apos;} ${err}`;
    } else {
      errMsg = error.message ? error.message : error.toString();
    }
    console.error(errMsg);
    return Observable.throw(errMsg);
  }
}
</code></pre>
<p>&#x9996;&#x5148;&#x5148;&#x6CE8;&#x5165; <code>http</code> &#x9032;&#x5165; <code>HttpClientService</code></p>
<pre><code>constructor (private http: Http) {}
</code></pre>
<p><code>url</code> &#x5C31;&#x662F;&#x8981; call &#x7684; API &#x4F4D;&#x7F6E;&#x3002;<br>
<code>http.get</code> &#x65B9;&#x6CD5;&#x8FD4;&#x56DE;&#x7684;&#x662F;&#x4E00;&#x500B; HTTP &#x97FF;&#x61C9; Observable &#x5C0D;&#x8C61;&#xFF0C;&#x7531; RxJS &#x5EAB;&#x63D0;&#x4F9B;&#xFF0C;<code>map()</code>&#x4E5F;&#x662F; RxJS &#x7684;&#x4E00;&#x500B;&#x64CD;&#x4F5C;&#x7B26;&#x3002;</p>
<h2>&#x8655;&#x7406;&#x56DE;&#x61C9;</h2>
<p>map()&#x51FD;&#x6578;&#x4E2D;&#xFF0C;&#x6211;&#x5011;&#x6703;&#x5C07;&#x63D0;&#x53D6;&#x6578;&#x64DA;&#x6620;&#x5C04;&#x5230; <code>this.extractData</code> &#x51FD;&#x6578;</p>
<pre><code>private extractData(res: Response) {
  if (res.status &lt; 200 || res.status &gt;= 300) {
    throw new Error(&apos;Bad response status: &apos; + res.status);
  }
  let body = res.json(); 
  return body.data || { };
}
</code></pre>
<p>Response &#x4E0D;&#x80FD;&#x76F4;&#x63A5;&#x7528;&#xFF0C;&#x8981;&#x5148;&#x9664;&#x932F;&#xFF0C;&#x4E26;&#x5C07;&#x8CC7;&#x6599;&#x8F49;&#x63DB;&#x6210; json &#x7D66;&#x7A0B;&#x5F0F;&#x4F7F;&#x7528;&#x3002;</p>
<h2>&#x4F7F;&#x7528;&#x8CC7;&#x6599;</h2>
<pre><code>getData() {
  this.HttpClientService.get(url:string)
                        .subscribe(
                          data =&gt; this.data = data,
                          error =&gt;  this.errorMessage = &lt;any&gt;error
                        );
}
</code></pre>
<h3>POST</h3>
<p>&#x65B9;&#x6CD5;&#x4E5F;&#x5927;&#x540C;&#x5C0F;&#x7570;</p>
<pre><code>post(url: string, body: any, optionHeader?: {[header: string]: string}): Observable&lt;Response&gt; {
    let headers = new Headers({&apos;Content-Type&apos;: &apos;application/x-www-form-urlencoded&apos;});
    // set option header
    for(let header in optionHeader) {
      let value = optionHeader[header];
      headers.append(header, value);
    }
    let newUrl = this.globalVariablesService.apiURL + url;
    return this.http.post(newUrl, body, {
      headers: headers,
    }).map(this.extractData)
      .catch(this.handleError);
}
</code></pre>
<h2>&#x53E6;&#x4E00;&#x7A2E;&#x5BEB;&#x6CD5;</h2>
<p>&#x4E8B;&#x5BE6;&#x4E0A;&#x6211;&#x5011;&#x4E5F;&#x53EF;&#x4EE5;&#x9019;&#x6A23;&#x5BEB;</p>
<pre><code>export class HttpClientService {
  ...
  get(url: string, optionHeader?: {[header: string]: string}): Observable&lt;Response&gt; {
    let headers = new Headers();
    // set option header
    for(let header in optionHeader) {
      let value = optionHeader[header];
      headers.append(header, value);
    }
    return this.http.get(url, {
      headers: headers,
    }).catch((res: Response) =&gt; this.handleError(res));
  }
  ...
}
</code></pre>
<p>&#x7576;&#x5176;&#x4ED6;&#x51FD;&#x6578;&#x8981;&#x8ABF;&#x7528; <code>get</code> &#x65B9;&#x6CD5;&#x6642;&#x6CE8;&#x5165;&#xFF0C;&#x4E14;&#x5148;&#x4E0D;&#x8655;&#x7406;&#x6210;&#x529F;&#x7684;&#x8CC7;&#x6599;&#x3002;</p>
<pre><code>getData(): void {
  let url = &apos;htts://...&apos;
  this.httpClientService.get(url)
      .subscribe(
        (res : Response) =&gt; {
          let data = res.json();
        },
        (err: any) =&gt; {
          console.log(&apos;err:&apos;,err);
        }
    );
}
</code></pre>
<p>&#x524D;&#x4E00;&#x7A2E;&#x5BEB;&#x6CD5;&#x9069;&#x5408;&#x5BEB;&#x660E;&#x78BA;&#x56DE;&#x50B3;&#x6771;&#x897F;&#x7684;&#x670D;&#x52D9;&#xFF0C;&#x5F8C;&#x8005;&#x9069;&#x5408;&#x5BEB;&#x901A;&#x7528;&#x578B;&#xFF0C;&#x53EF;&#x4EE5;&#x63A5;&#x53D7;&#x4EFB;&#x4F55;&#x8CC7;&#x6599;&#xFF0C;&#x6700;&#x5F8C;&#x5728;&#x8F49;&#x63DB;&#x3002;&#x4E0D;&#x7BA1;&#x54EA;&#x4E00;&#x7A2E;&#x5BEB;&#x6CD5;&#x90FD;&#x662F;&#x5C07; <code>http</code> &#x65B9;&#x6CD5;&#x548C;&#x8981;&#x6700;&#x5F8C;&#x8655;&#x7406;&#x7684;&#x5DE5;&#x4F5C;&#x505A;&#x5340;&#x9694;&#xFF0C;&#x767C;&#x751F;&#x932F;&#x8AA4;&#x6642;&#x53EF;&#x4EE5;&#x5340;&#x5206;&#x662F; <code>http</code> &#x51FA;&#x932F;&#x9084;&#x662F; <code>getData()</code>&#x51FA;&#x932F;&#xFF0C;&#x53D6;&#x5230;&#x8CC7;&#x6599;&#x5F8C;&#x53EF;&#x4EE5;&#x518D;&#x62FF;&#x4F86;&#x505A;&#x5176;&#x4ED6;&#x4E8B;&#x60C5;&#x3002;&#x7C21;&#x55AE;&#x4F86;&#x8AAA;&#x5C31;&#x662F;&#x5C07;&#x7A0B;&#x5F0F;&#x505A;&#x5C64;&#x7D1A;&#x5316;&#xFF0C;&#x908F;&#x8F2F;&#x6839;&#x7BA1;&#x7406;&#x90FD;&#x6BD4;&#x8F03;&#x5BB9;&#x6613;&#x3002;</p>
<h2>AJAX</h2>
<p>&#x7576;&#x7136;&#x9664;&#x4E86; Angular &#x5B98;&#x65B9;&#x63D0;&#x4F9B;&#x7684;&#x65B9;&#x6CD5;&#xFF0C;AJAX &#x9084;&#x662F;&#x4E00;&#x6A23;&#x53D7;&#x5927;&#x5BB6;&#x611B;&#x6234;&#x3002;<br>
&#x6C92;&#x4EC0;&#x9EBC;&#x6280;&#x8853;&#x597D;&#x8AAA;&#x7684;&#xFF0C;&#x4E00;&#x6A23;&#x662F;&#x7570;&#x6B65;&#xFF0C;&#x800C;&#x4E14;&#x8A18;&#x5F97;&#x8981;&#x5F15;&#x5165; jQuery&#x3002;&#x6BD4;&#x8F03;&#x9EBB;&#x7169;&#x7684;&#x662F; TSlint &#x770B;&#x4E0D;&#x61C2; <code>$</code>&#xFF0C;&#x6240;&#x4EE5;&#x53EF;&#x4EE5;&#x5F88;&#x4F5C;&#x5F0A;&#x7684;&#x9019;&#x6A23;&#x505A;&#x3002;<code>declare var $:any;</code>&#x653E;&#x5728; ts &#x6700;&#x524D;&#x9762;&#x3002;</p>
<pre><code>$.ajax({
  url: url,
  type: &apos;POST&apos;,
  data:  {&apos;data&apos;:JSON.stringify(json)},
  success: function(data: any) {
      console.log(data);
  },
  error: function(XMLHttpRequest: any, textStatus: any, errorThrown: any) {
      console.log(errorThrown);
  }
});
</code></pre>
<p>AJAX &#x5C31;&#x4E0D;&#x591A;&#x8AAA;&#x751A;&#x9EBC;&#x4E86;&#xFF0C;&#x7E3D;&#x4E4B;&#x4E5F;&#x662F;&#x500B;&#x65B9;&#x6CD5;&#x3002;</p>
 <br>
                                                    </div>
                    </div>
                
