Download Link: https://assignmentchef.com/product/solved-assignment-05-shape-animation
<br>
<h2><a id="user-content-requirements" class="anchor" href="https://github.com/timferido/assignment-05#requirements" aria-hidden="true"></a>Requirements</h2>

<ul>

 <li>Write the following classes:

  <ul>

   <li><code>Point</code>

    <ul>

     <li>Describes a point in the Euclidean plane.

      <ul>

       <li>Note: This means that the x and y values need to be either <code>float</code> or <code>double</code>.</li>

      </ul></li>

     <li>Must be able to be initialized with no arguments, defaulting to the point (0,0).

      <ul>

       <li>Note: This is the same as saying that it must have a default constructor. If a constructor has default values for all arguments, it fulfills this requirement and is considered a default constructor.</li>

      </ul></li>

     <li>Must be able to be initialized with an x and y value.</li>

     <li>Must not be possible to change the x or y value once it has been constructed.

      <ul>

       <li>Note: This means that the member variables containing the x and y values must be private (or protected), and you must implement getters (but not setters) for each.</li>

      </ul></li>

    </ul></li>

   <li><code>Shape</code>

    <ul>

     <li>Must contain the following pure virtual function:</li>

     <li>Should also contain a virtual default destructor:This allows for child classes being handled through a pointer of type <code>Shape</code> to have their destructors called when the variable goes out of scope or is <code>delete</code>d (search “cpp polymorphism”).</li>

    </ul></li>

   <li><code>Rectangle</code> and <code>Ellipse</code>

    <ul>

     <li>Must inherit from <code>Shape</code>, and be concrete classes (i.e. not abstract classes, i.e. they must override all <code>Shape</code>s pure virtual functions).</li>

    </ul></li>

   <li><code>Square</code>

    <ul>

     <li>Must inherit from <code>Rectangle</code>.</li>

    </ul></li>

   <li><code>Circle</code>

    <ul>

     <li>Must inherit from <code>Ellipse</code>.</li>

    </ul></li>

  </ul></li>

 <li>Write a function with the following prototype (probably in <code>main.cpp</code>):This function should iterate through every column on every line. If the point represented by the character at that location is contained in any of the <code>Shape</code>s, it should print a <code>"*"</code> (or something). If not, it should print a <code>" "</code> (or something).This function should also scale the shapes correctly, according the aspect ratio of the terminal characters. It would probably be best to use several constants: one to represent the number of columns, one to represent the factor used to convert the column number to the x value represented by a character in that column, and similarly for the number of lines and the factor used to convert the line number to the corresponding y value.Optionally, you may also draw a border, where the top and bottom of each column is a <code>"-"</code> (or something), and the first and last character of each line is a <code>"|"</code> (or something).</li>

 <li>Use the following template for <code>main()</code>:If you’d like to write your <code>main()</code> in a different way that’s fine, so long as it accomplishes the same goal.</li>

</ul>

<h2><a id="user-content-requests" class="anchor" href="https://github.com/timferido/assignment-05#requests" aria-hidden="true"></a>Requests</h2>

<ul>

 <li>Please try to do this in groups, and try to use Google, etc., only for answers to questions about the language (as opposed to questions about this problem).</li>

</ul>

<h2><a id="user-content-assumptions" class="anchor" href="https://github.com/timferido/assignment-05#assumptions" aria-hidden="true"></a>Assumptions</h2>

<ul>

 <li>A terminal window is 80 columns wide by 25 lines high.</li>

 <li>The width:height aspect ratio of a terminal character is approximately 1:1.9.</li>

</ul>

<h2><a id="user-content-style" class="anchor" href="https://github.com/timferido/assignment-05#style" aria-hidden="true"></a>Style</h2>

<ul>

 <li>Place your solution in a <code>solution--YOURNAME</code> subdirectory (where <code>YOURNAME</code> is your GitHub username).</li>

 <li>Include your copyright and license information at the top of every file, followed by a brief description of the file’s contents, e.g.</li>

 <li>Use “include guards” in all <code>.h</code> files. Be sure to give the preprocessor variable a name corresponding to the file name. For example, in <code>point.h</code>:</li>

 <li><code>main()</code> must have its own <code>.cpp</code> file. I suggest calling it <code>main.cpp</code>.</li>

 <li>Classes must have both <code>.h</code> and <code>.cpp</code> files, with member functions defined in the <code>.cpp</code> files unless they are truly trivial. If it makes sense, you may put multiple classes into one pair of <code>.h</code> and <code>.cpp</code> files.</li>

 <li>Declare member functions and function arguments as <code>const</code> when appropriate (in general, whenever possible).</li>

 <li>Document and format your code well and consistently. Be sure to clearly document the source of any code, algorithm, information, etc. that you use or reference while completing your work.</li>

 <li>Wrap lines at 79 or 80 columns whenever possible.</li>

 <li>End your file with a blank line.</li>

 <li>Do <em>not</em> use <code>using namespace std;</code>. You may get around typing <code>std::</code> in front of things or with, e.g., <code>using std::cout;</code>.</li>

</ul>

5/5 - (2 votes)

<pre><span class="pl-c">/**</span><span class="pl-c"> * A function to determine whether a shape contains a given point.</span><span class="pl-c"> *</span><span class="pl-c"> * Arguments:</span><span class="pl-c"> * - `p`: The point we are considering.</span><span class="pl-c"> *</span><span class="pl-c"> * Returns:</span><span class="pl-c"> * - `true` if the given point is inside the shape, `false`</span><span class="pl-c"> *   otherwise.</span><span class="pl-c"> */</span><span class="pl-k">virtual</span> <span class="pl-k">bool</span> <span class="pl-en">contains</span>(<span class="pl-k">const</span> <span class="pl-c1">Point</span> &amp; p) <span class="pl-k">const</span> = 0;</pre>

<pre><span class="pl-k">virtual</span> <span class="pl-en">~Shape</span>() = <span class="pl-k">default</span>;</pre>

<pre><span class="pl-c">/**</span><span class="pl-c"> * A function to draw the `Shape*`s in the given vector in a terminal.</span><span class="pl-c"> *</span><span class="pl-c"> * Arguments:</span><span class="pl-c"> * - `v`: A vector containing pointers to each `Shape` to draw.</span><span class="pl-c"> *</span><span class="pl-c"> * Notes:</span><span class="pl-c"> * - A terminal window is typically 80 columns wide by 25 lines high.</span><span class="pl-c"> * - The width:height aspect ratio of a terminal character is approximately</span><span class="pl-c"> *   1:1.9.</span><span class="pl-c"> */</span><span class="pl-k">void</span> <span class="pl-en">draw</span>(<span class="pl-k">const</span> vector&lt;Shape*&gt; &amp; v) {</pre>

<pre><span class="pl-k">int</span> <span class="pl-en">main</span>() {    <span class="pl-c">// declare constants for the number of frames to draw and the</span>    <span class="pl-c">// amount of time to sleep after drawing each frame</span>    <span class="pl-c">// for each frame</span>        <span class="pl-c">// create some shapes (with values depending on the current frame</span>        <span class="pl-c">// number)</span>        <span class="pl-c">// put pointers to them in an array</span>        <span class="pl-c">//</span>        <span class="pl-c">// for example, given a `Rectangle r` and a `Square s`:</span>        vector&lt;Shape*&gt; shapes = { &amp;r, &amp;s, };        <span class="pl-c">// this is possible because `Rectangle`s and `Squares`, and all</span>        <span class="pl-c">// your other shapes, inherit from `Shape`</span>        <span class="pl-c">// draw the shapes in the terminal</span>        <span class="pl-c">//</span>        <span class="pl-c">// for example, given the `shapes` array above:</span>        <span class="pl-c1">draw</span>(shapes);        <span class="pl-c">// wait before drawing the next frame</span>        <span class="pl-c">//</span>        <span class="pl-c">// for example:</span>        <span class="pl-c1">std::this_thread::sleep_for</span>(<span class="pl-c1">std::chrono::milliseconds</span>(frameSleep));        <span class="pl-c">// if you'd like to know more about what this line is doing, look</span>        <span class="pl-c">// up the documentation for `std::this_thread::sleep_for` and</span>        <span class="pl-c">// `std::chrono::milliseconds()`.</span>    <span class="pl-k">return</span> <span class="pl-c1">0</span>;  <span class="pl-c">// success</span>}</pre>

<pre><span class="pl-c">/* ----------------------------------------------------------------------------</span><span class="pl-c"> * Copyright &amp;copy; 2016 Ben Blazak &lt;<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="24464648455e454f64425148484156504b4a0a414051">[email protected]</a>&gt;</span><span class="pl-c"> * Released under the [MIT License] (http://opensource.org/licenses/MIT)</span><span class="pl-c"> * ------------------------------------------------------------------------- */</span><span class="pl-c">/**</span><span class="pl-c"> * A short program to print "Hello World!" to standard output.</span><span class="pl-c"> */</span></pre>