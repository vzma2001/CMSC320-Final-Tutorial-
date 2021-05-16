<<<<<<< HEAD
<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">from</span> <span class="nn">os</span> <span class="kn">import</span> <span class="n">listdir</span>
<span class="kn">from</span> <span class="nn">os.path</span> <span class="kn">import</span> <span class="n">isfile</span><span class="p">,</span> <span class="n">join</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span> 
<span class="kn">import</span> <span class="nn">datetime</span>
<span class="kn">import</span> <span class="nn">itertools</span>
<span class="kn">from</span> <span class="nn">matplotlib.patches</span> <span class="kn">import</span> <span class="n">Patch</span>
<span class="kn">from</span> <span class="nn">matplotlib.lines</span> <span class="kn">import</span> <span class="n">Line2D</span>
<span class="kn">import</span> <span class="nn">matplotlib.ticker</span> <span class="k">as</span> <span class="nn">ticker</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LinearRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>
<span class="kn">import</span> <span class="nn">statsmodels.api</span> <span class="k">as</span> <span class="nn">sm</span>
<span class="kn">from</span> <span class="nn">scipy</span> <span class="kn">import</span> <span class="n">stats</span>
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">from</span> <span class="nn">IPython.display</span> <span class="kn">import</span> <span class="n">Image</span>
<span class="kn">from</span> <span class="nn">base64</span> <span class="kn">import</span> <span class="n">b64decode</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [3]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Go though Web Export, split on ;</span>
<span class="nb">id</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">label</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Id'</span><span class="p">,</span><span class="s1">'Banner'</span><span class="p">,</span><span class="s1">'Item'</span><span class="p">,</span><span class="s1">'Type'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">,</span><span class="s1">'Date'</span><span class="p">]</span>
<span class="n">rolls</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="n">label</span><span class="p">)</span>
<span class="n">web_dir</span> <span class="o">=</span> <span class="s2">"C:/Users/vzma/spring2021/CMSC320-Final-Tutorial/Data/WebExport"</span>
<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">listdir</span><span class="p">(</span><span class="n">web_dir</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">isfile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">web_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">)):</span>
        <span class="n">curr</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">web_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">index</span><span class="p">,</span><span class="n">line</span> <span class="ow">in</span> <span class="n">curr</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
            <span class="n">temp</span> <span class="o">=</span> <span class="n">line</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">';'</span><span class="p">)</span>
            <span class="n">b</span> <span class="o">=</span> <span class="n">temp</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
            <span class="k">if</span> <span class="n">b</span><span class="o">==</span><span class="s2">"Character Event"</span><span class="p">:</span>
                <span class="n">b</span> <span class="o">=</span> <span class="s2">"Event"</span>
            <span class="k">elif</span> <span class="n">b</span><span class="o">==</span><span class="s2">"Weapon Event"</span><span class="p">:</span>
                <span class="n">b</span> <span class="o">=</span> <span class="s2">"Weapon"</span>
            <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="nb">id</span><span class="p">,</span><span class="n">b</span><span class="p">,</span><span class="n">temp</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span><span class="n">temp</span><span class="p">[</span><span class="mi">3</span><span class="p">],</span><span class="nb">int</span><span class="p">(</span><span class="n">temp</span><span class="p">[</span><span class="mi">4</span><span class="p">]),</span><span class="n">temp</span><span class="p">[</span><span class="mi">5</span><span class="p">][:</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">replace</span><span class="p">(</span><span class="s1">'T'</span><span class="p">,</span> <span class="s1">' '</span><span class="p">)]</span>
            <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
        <span class="nb">id</span> <span class="o">=</span> <span class="nb">id</span><span class="o">+</span><span class="mi">1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [4]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Go though External Export get rid of stars</span>
<span class="n">ext_dir</span> <span class="o">=</span> <span class="s2">"C:/Users/vzma/spring2021/CMSC320-Final-Tutorial/Data/ExternalExport"</span>
<span class="n">b</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Character Event Wish History'</span><span class="p">,</span> <span class="s1">'Permanent Wish History'</span><span class="p">,</span> <span class="s1">'Weapon Event Wish History'</span><span class="p">,</span> <span class="s1">'Novice Wish History'</span><span class="p">]</span>
<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">listdir</span><span class="p">(</span><span class="n">ext_dir</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">isfile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">ext_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">)):</span>
        <span class="n">notebook</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">ext_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">sheet</span> <span class="ow">in</span> <span class="n">b</span><span class="p">:</span>
            <span class="n">curr</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span><span class="n">notebook</span><span class="p">,</span><span class="n">sheet_name</span><span class="o">=</span><span class="n">sheet</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">index</span><span class="p">,</span><span class="n">line</span> <span class="ow">in</span> <span class="n">curr</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
                <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="nb">id</span><span class="p">,</span><span class="n">line</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Item Name'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Item Type'</span><span class="p">],</span><span class="nb">len</span><span class="p">(</span><span class="n">line</span><span class="p">[</span><span class="s1">'Item Rarity'</span><span class="p">]),</span><span class="n">line</span><span class="p">[</span><span class="s1">'Date and Time'</span><span class="p">]]</span>
                <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
        <span class="nb">id</span> <span class="o">=</span> <span class="nb">id</span><span class="o">+</span><span class="mi">1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [5]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Find Chinese document and figure out if it can be translated or just trash</span>
<span class="n">name_dir</span> <span class="o">=</span> <span class="s2">"C:/Users/vzma/spring2021/CMSC320-Final-Tutorial/Data/Export/rewardname"</span>
<span class="n">b</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Character Event Wish'</span><span class="p">,</span> <span class="s1">'Permanent Wish'</span><span class="p">,</span> <span class="s1">'Weapon Event Wish'</span><span class="p">,</span> <span class="s1">'Novice Wishes'</span><span class="p">]</span>
<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">listdir</span><span class="p">(</span><span class="n">name_dir</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">isfile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">name_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">)):</span>
        <span class="n">notebook</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">name_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">sheet</span> <span class="ow">in</span> <span class="n">b</span><span class="p">:</span>
            <span class="n">curr</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span><span class="n">notebook</span><span class="p">,</span><span class="n">sheet_name</span><span class="o">=</span><span class="n">sheet</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">index</span><span class="p">,</span><span class="n">line</span> <span class="ow">in</span> <span class="n">curr</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
                <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="nb">id</span><span class="p">,</span><span class="n">line</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Reward Name'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Reward Type'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Rarity (Star)'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'Timestamp'</span><span class="p">]]</span>
                <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
        <span class="nb">id</span> <span class="o">=</span> <span class="nb">id</span><span class="o">+</span><span class="mi">1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">main_dir</span> <span class="o">=</span> <span class="s2">"C:/Users/vzma/spring2021/CMSC320-Final-Tutorial/Data/Export/name"</span>
<span class="n">b</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Character Event Wish'</span><span class="p">,</span> <span class="s1">'Permanent Wish'</span><span class="p">,</span> <span class="s1">'Weapon Event Wish'</span><span class="p">,</span> <span class="s1">'Novice Wishes'</span><span class="p">]</span>
<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">listdir</span><span class="p">(</span><span class="n">main_dir</span><span class="p">):</span>
    <span class="k">if</span> <span class="n">isfile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">main_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">)):</span>
        <span class="n">notebook</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">ExcelFile</span><span class="p">(</span><span class="n">join</span><span class="p">(</span><span class="n">main_dir</span><span class="p">,</span> <span class="n">f</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">sheet</span> <span class="ow">in</span> <span class="n">b</span><span class="p">:</span>
            <span class="n">curr</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span><span class="n">notebook</span><span class="p">,</span><span class="n">sheet_name</span><span class="o">=</span><span class="n">sheet</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">index</span><span class="p">,</span><span class="n">line</span> <span class="ow">in</span> <span class="n">curr</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
                <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="nb">id</span><span class="p">,</span><span class="n">line</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'name'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'type'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'rarity'</span><span class="p">],</span><span class="n">line</span><span class="p">[</span><span class="s1">'time'</span><span class="p">]]</span>
                <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
        <span class="nb">id</span> <span class="o">=</span> <span class="nb">id</span><span class="o">+</span><span class="mi">1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [7]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span> <span class="o">=</span> <span class="n">rolls</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">'datetime64[ns]'</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="mi">2</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Weapon'</span><span class="p">][</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[8]:</div>

<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">

<pre>array([3, 4, 5], dtype=object)</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">weapons</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">,</span><span class="s1">'Count'</span><span class="p">])</span>
<span class="n">temp</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Weapon'</span><span class="p">]</span><span class="o">.</span><span class="n">Item</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="k">for</span> <span class="n">w</span> <span class="ow">in</span> <span class="n">temp</span><span class="p">:</span>
    <span class="n">r</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="n">w</span><span class="p">]</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">r</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="n">w</span><span class="p">,</span> <span class="n">x</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">r</span><span class="p">)]</span>
    <span class="n">weapons</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">weapons</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">weapons</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s1">'Count'</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[10]:</div>

<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Item</th>

<th>Rarity</th>

<th>Count</th>

</tr>

</thead>

<tbody>

<tr>

<th>15</th>

<td>Skyrider Sword</td>

<td>3</td>

<td>1467</td>

</tr>

<tr>

<th>3</th>

<td>Bloodtainted Greatsword</td>

<td>3</td>

<td>1466</td>

</tr>

<tr>

<th>5</th>

<td>Sharpshooter's Oath</td>

<td>3</td>

<td>1463</td>

</tr>

<tr>

<th>7</th>

<td>Black Tassel</td>

<td>3</td>

<td>1414</td>

</tr>

<tr>

<th>2</th>

<td>Ferrous Shadow</td>

<td>3</td>

<td>1413</td>

</tr>

<tr>

<th>8</th>

<td>Slingshot</td>

<td>3</td>

<td>1388</td>

</tr>

<tr>

<th>4</th>

<td>Thrilling Tales of Dragon Slayers</td>

<td>3</td>

<td>1387</td>

</tr>

<tr>

<th>11</th>

<td>Emerald Orb</td>

<td>3</td>

<td>1365</td>

</tr>

<tr>

<th>6</th>

<td>Harbinger of Dawn</td>

<td>3</td>

<td>1358</td>

</tr>

<tr>

<th>0</th>

<td>Raven Bow</td>

<td>3</td>

<td>1348</td>

</tr>

<tr>

<th>1</th>

<td>Magic Guide</td>

<td>3</td>

<td>1342</td>

</tr>

<tr>

<th>12</th>

<td>Debate Club</td>

<td>3</td>

<td>1336</td>

</tr>

<tr>

<th>9</th>

<td>Cool Steel</td>

<td>3</td>

<td>1300</td>

</tr>

<tr>

<th>21</th>

<td>Dragon's Bane</td>

<td>4</td>

<td>104</td>

</tr>

<tr>

<th>14</th>

<td>Eye of Perception</td>

<td>4</td>

<td>101</td>

</tr>

<tr>

<th>24</th>

<td>Favonius Lance</td>

<td>4</td>

<td>86</td>

</tr>

<tr>

<th>31</th>

<td>Lion's Roar</td>

<td>4</td>

<td>77</td>

</tr>

<tr>

<th>18</th>

<td>Sacrificial Bow</td>

<td>4</td>

<td>75</td>

</tr>

<tr>

<th>17</th>

<td>Sacrificial Greatsword</td>

<td>4</td>

<td>75</td>

</tr>

<tr>

<th>10</th>

<td>Sacrificial Sword</td>

<td>4</td>

<td>72</td>

</tr>

<tr>

<th>28</th>

<td>Rust</td>

<td>4</td>

<td>71</td>

</tr>

<tr>

<th>30</th>

<td>The Flute</td>

<td>4</td>

<td>70</td>

</tr>

<tr>

<th>16</th>

<td>Favonius Warbow</td>

<td>4</td>

<td>66</td>

</tr>

<tr>

<th>19</th>

<td>The Widsith</td>

<td>4</td>

<td>64</td>

</tr>

<tr>

<th>20</th>

<td>Favonius Codex</td>

<td>4</td>

<td>63</td>

</tr>

<tr>

<th>26</th>

<td>Sacrificial Fragments</td>

<td>4</td>

<td>59</td>

</tr>

<tr>

<th>32</th>

<td>The Bell</td>

<td>4</td>

<td>54</td>

</tr>

<tr>

<th>23</th>

<td>The Stringless</td>

<td>4</td>

<td>53</td>

</tr>

<tr>

<th>29</th>

<td>Favonius Greatsword</td>

<td>4</td>

<td>43</td>

</tr>

<tr>

<th>13</th>

<td>Favonius Sword</td>

<td>4</td>

<td>43</td>

</tr>

<tr>

<th>34</th>

<td>Rainslasher</td>

<td>4</td>

<td>39</td>

</tr>

<tr>

<th>40</th>

<td>Lithic Blade</td>

<td>4</td>

<td>31</td>

</tr>

<tr>

<th>41</th>

<td>Lithic Spear</td>

<td>4</td>

<td>28</td>

</tr>

<tr>

<th>35</th>

<td>Skyward Pride</td>

<td>5</td>

<td>18</td>

</tr>

<tr>

<th>33</th>

<td>Wolf's Gravestone</td>

<td>5</td>

<td>16</td>

</tr>

<tr>

<th>39</th>

<td>Primordial Jade Winged-Spear</td>

<td>5</td>

<td>13</td>

</tr>

<tr>

<th>43</th>

<td>Primordial Jade Cutter</td>

<td>5</td>

<td>12</td>

</tr>

<tr>

<th>36</th>

<td>Amos' Bow</td>

<td>5</td>

<td>10</td>

</tr>

<tr>

<th>25</th>

<td>Skyward Blade</td>

<td>5</td>

<td>9</td>

</tr>

<tr>

<th>42</th>

<td>Staff of Homa</td>

<td>5</td>

<td>8</td>

</tr>

<tr>

<th>44</th>

<td>Skyward Harp</td>

<td>5</td>

<td>7</td>

</tr>

<tr>

<th>22</th>

<td>Skyward Atlas</td>

<td>5</td>

<td>7</td>

</tr>

<tr>

<th>45</th>

<td>Skyward Spine</td>

<td>5</td>

<td>5</td>

</tr>

<tr>

<th>27</th>

<td>Lost Prayer to the Sacred Winds</td>

<td>5</td>

<td>5</td>

</tr>

<tr>

<th>38</th>

<td>Aquila Favonia</td>

<td>5</td>

<td>5</td>

</tr>

<tr>

<th>37</th>

<td>Summit Shaper</td>

<td>5</td>

<td>2</td>

</tr>

<tr>

<th>46</th>

<td>Memory of Dust</td>

<td>5</td>

<td>1</td>

</tr>

<tr>

<th>47</th>

<td>The Unforged</td>

<td>5</td>

<td>1</td>

</tr>

<tr>

<th>48</th>

<td>Vortex Vanquisher</td>

<td>5</td>

<td>1</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">characters</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'Character'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">,</span><span class="s1">'Count'</span><span class="p">])</span>
<span class="n">temp</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Character'</span><span class="p">]</span><span class="o">.</span><span class="n">Item</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="k">for</span> <span class="n">w</span> <span class="ow">in</span> <span class="n">temp</span><span class="p">:</span>
    <span class="n">r</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="n">w</span><span class="p">]</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">r</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
    <span class="n">to_add</span> <span class="o">=</span> <span class="p">[</span><span class="n">w</span><span class="p">,</span> <span class="n">x</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">r</span><span class="p">)]</span>
    <span class="n">characters</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">characters</span><span class="o">.</span><span class="n">index</span><span class="p">)]</span> <span class="o">=</span> <span class="n">to_add</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [12]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">characters</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s1">'Count'</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[12]:</div>

<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Character</th>

<th>Rarity</th>

<th>Count</th>

</tr>

</thead>

<tbody>

<tr>

<th>6</th>

<td>Xiangling</td>

<td>4</td>

<td>207</td>

</tr>

<tr>

<th>19</th>

<td>Xingqiu</td>

<td>4</td>

<td>160</td>

</tr>

<tr>

<th>0</th>

<td>Noelle</td>

<td>4</td>

<td>157</td>

</tr>

<tr>

<th>10</th>

<td>Sucrose</td>

<td>4</td>

<td>126</td>

</tr>

<tr>

<th>1</th>

<td>Chongyun</td>

<td>4</td>

<td>121</td>

</tr>

<tr>

<th>2</th>

<td>Fischl</td>

<td>4</td>

<td>117</td>

</tr>

<tr>

<th>16</th>

<td>Xinyan</td>

<td>4</td>

<td>111</td>

</tr>

<tr>

<th>18</th>

<td>Beidou</td>

<td>4</td>

<td>100</td>

</tr>

<tr>

<th>12</th>

<td>Barbara</td>

<td>4</td>

<td>95</td>

</tr>

<tr>

<th>14</th>

<td>Razor</td>

<td>4</td>

<td>88</td>

</tr>

<tr>

<th>5</th>

<td>Bennett</td>

<td>4</td>

<td>82</td>

</tr>

<tr>

<th>13</th>

<td>Diona</td>

<td>4</td>

<td>76</td>

</tr>

<tr>

<th>21</th>

<td>Ningguang</td>

<td>4</td>

<td>56</td>

</tr>

<tr>

<th>8</th>

<td>Lisa</td>

<td>4</td>

<td>42</td>

</tr>

<tr>

<th>17</th>

<td>Keqing</td>

<td>5</td>

<td>37</td>

</tr>

<tr>

<th>3</th>

<td>Kaeya</td>

<td>4</td>

<td>28</td>

</tr>

<tr>

<th>20</th>

<td>Qiqi</td>

<td>5</td>

<td>23</td>

</tr>

<tr>

<th>26</th>

<td>Ganyu</td>

<td>5</td>

<td>20</td>

</tr>

<tr>

<th>9</th>

<td>Diluc</td>

<td>5</td>

<td>19</td>

</tr>

<tr>

<th>25</th>

<td>Mona</td>

<td>5</td>

<td>18</td>

</tr>

<tr>

<th>11</th>

<td>Venti</td>

<td>5</td>

<td>17</td>

</tr>

<tr>

<th>4</th>

<td>Jean</td>

<td>5</td>

<td>17</td>

</tr>

<tr>

<th>15</th>

<td>Zhongli</td>

<td>5</td>

<td>15</td>

</tr>

<tr>

<th>27</th>

<td>Xiao</td>

<td>5</td>

<td>15</td>

</tr>

<tr>

<th>7</th>

<td>Amber</td>

<td>4</td>

<td>13</td>

</tr>

<tr>

<th>22</th>

<td>Klee</td>

<td>5</td>

<td>11</td>

</tr>

<tr>

<th>23</th>

<td>Tartaglia</td>

<td>5</td>

<td>10</td>

</tr>

<tr>

<th>24</th>

<td>Albedo</td>

<td>5</td>

<td>9</td>

</tr>

<tr>

<th>28</th>

<td>Hu Tao</td>

<td>5</td>

<td>9</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [13]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="c1">#Heat map of items and version/banner? to show how common each item is</span>
<span class="c1">#line graph that shows number of rolls over time; demonstrate which banner is wanted most</span>
<span class="c1">#pi chart for each person</span>
<span class="c1">#histogram of pity</span>

<span class="n">versions</span> <span class="o">=</span> <span class="p">{}</span>
<span class="n">versions</span><span class="p">[</span><span class="s1">'v1.0'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-09-28 00:00:00"</span><span class="p">,</span> <span class="s2">"2020-11-11 16:00:00"</span><span class="p">]</span>
<span class="n">versions</span><span class="p">[</span><span class="s1">'v1.1'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-11-11 16:00:01"</span><span class="p">,</span> <span class="s2">"2020-12-23 16:00:00"</span><span class="p">]</span>
<span class="n">versions</span><span class="p">[</span><span class="s1">'v1.2'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-12-23 16:00:01"</span><span class="p">,</span> <span class="s2">"2021-02-03 16:00:00"</span><span class="p">]</span>
<span class="n">versions</span><span class="p">[</span><span class="s1">'v1.3'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-02-03 16:00:01"</span><span class="p">,</span> <span class="s2">"2021-03-17 16:00:00"</span><span class="p">]</span>
<span class="k">for</span> <span class="n">key</span> <span class="ow">in</span> <span class="n">versions</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
    <span class="n">start</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">strptime</span><span class="p">(</span><span class="n">versions</span><span class="p">[</span><span class="n">key</span><span class="p">][</span><span class="mi">0</span><span class="p">],</span> <span class="s1">'%Y-%m-</span><span class="si">%d</span> <span class="s1">%H:%M:%S'</span><span class="p">)</span>
    <span class="n">end</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">strptime</span><span class="p">(</span><span class="n">versions</span><span class="p">[</span><span class="n">key</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> <span class="s1">'%Y-%m-</span><span class="si">%d</span> <span class="s1">%H:%M:%S'</span><span class="p">)</span>

    <span class="n">versions</span><span class="p">[</span><span class="n">key</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="n">start</span><span class="p">,</span> <span class="n">end</span><span class="p">]</span>

<span class="n">charbanners</span> <span class="o">=</span> <span class="p">{}</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Venti'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-09-28 00:00:00"</span><span class="p">,</span> <span class="s2">"2020-10-18 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Klee'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-10-18 16:00:01"</span><span class="p">,</span><span class="s2">"2020-11-10 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Childe'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-11-10 16:00:01"</span><span class="p">,</span><span class="s2">"2020-11-30 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Zhongli'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-11-30 16:00:01"</span><span class="p">,</span><span class="s2">"2020-12-23 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Albedo'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2020-12-23 16:00:01"</span><span class="p">,</span><span class="s2">"2021-01-12 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Ganyu'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-01-12 16:00:01"</span><span class="p">,</span><span class="s2">"2021-02-02 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Xiao'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-02-02 16:00:01"</span><span class="p">,</span><span class="s2">"2021-02-17 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Keqing'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-02-17 16:00:01"</span><span class="p">,</span><span class="s2">"2021-03-02 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Hutao'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-03-02 16:00:01"</span><span class="p">,</span><span class="s2">"2021-03-17 16:00:00"</span><span class="p">]</span>
<span class="n">charbanners</span><span class="p">[</span><span class="s1">'Venti2.0'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"2021-03-16 16:00:01"</span><span class="p">,</span><span class="s2">"2021-04-06 16:00:00"</span><span class="p">]</span>
<span class="k">for</span> <span class="n">key</span> <span class="ow">in</span> <span class="n">charbanners</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
    <span class="n">start</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">strptime</span><span class="p">(</span><span class="n">charbanners</span><span class="p">[</span><span class="n">key</span><span class="p">][</span><span class="mi">0</span><span class="p">],</span> <span class="s1">'%Y-%m-</span><span class="si">%d</span> <span class="s1">%H:%M:%S'</span><span class="p">)</span>
    <span class="n">end</span> <span class="o">=</span> <span class="n">datetime</span><span class="o">.</span><span class="n">datetime</span><span class="o">.</span><span class="n">strptime</span><span class="p">(</span><span class="n">charbanners</span><span class="p">[</span><span class="n">key</span><span class="p">][</span><span class="mi">1</span><span class="p">],</span> <span class="s1">'%Y-%m-</span><span class="si">%d</span> <span class="s1">%H:%M:%S'</span><span class="p">)</span>
    <span class="n">charbanners</span><span class="p">[</span><span class="n">key</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="n">start</span><span class="p">,</span> <span class="n">end</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">eventrolls</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span>
<span class="n">eventrolls</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s1">'Date'</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">counter</span> <span class="o">=</span> <span class="p">{}</span>
<span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">eventrolls</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
    <span class="n">to_add</span> <span class="o">=</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span><span class="o">.</span><span class="n">date</span><span class="p">()</span>
    <span class="k">if</span> <span class="n">to_add</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">counter</span><span class="p">:</span>
        <span class="n">counter</span><span class="p">[</span><span class="n">to_add</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">counter</span><span class="p">[</span><span class="n">to_add</span><span class="p">]</span> <span class="o">=</span> <span class="n">counter</span><span class="p">[</span><span class="n">to_add</span><span class="p">]</span> <span class="o">+</span> <span class="mi">1</span>
<span class="n">x</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">y</span> <span class="o">=</span> <span class="p">[]</span>

<span class="k">for</span> <span class="n">key</span> <span class="ow">in</span> <span class="n">counter</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
    <span class="n">x</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">key</span><span class="p">)</span>
    <span class="n">y</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">counter</span><span class="p">[</span><span class="n">key</span><span class="p">])</span>

<span class="n">x</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="nb">zip</span><span class="p">(</span><span class="o">*</span><span class="nb">sorted</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Total Event Rolls"</span><span class="p">)</span>
<span class="n">c</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'springgreen'</span><span class="p">,</span> <span class="s1">'lightcoral'</span><span class="p">,</span><span class="s1">'cornflowerblue'</span><span class="p">,</span><span class="s1">'goldenrod'</span><span class="p">,</span><span class="s1">'bisque'</span><span class="p">,</span><span class="s1">'lightskyblue'</span><span class="p">,</span><span class="s1">'mediumaquamarine'</span><span class="p">,</span><span class="s1">'mediumslateblue'</span><span class="p">,</span><span class="s1">'indianred'</span><span class="p">,</span><span class="s1">'forestgreen'</span><span class="p">]</span>

<span class="n">i</span><span class="o">=</span><span class="mi">0</span>
<span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="n">charbanners</span><span class="o">.</span><span class="n">keys</span><span class="p">():</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">axvspan</span><span class="p">(</span><span class="n">charbanners</span><span class="p">[</span><span class="n">k</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">date</span><span class="p">(),</span> <span class="n">charbanners</span><span class="p">[</span><span class="n">k</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">date</span><span class="p">(),</span> <span class="n">color</span><span class="o">=</span><span class="n">c</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> <span class="n">lw</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">i</span><span class="o">=</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span>

<span class="n">legend_elements</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">i</span><span class="o">=</span><span class="mi">0</span>
<span class="n">keys</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">charbanners</span><span class="o">.</span><span class="n">keys</span><span class="p">())</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">c</span><span class="p">)):</span>
    <span class="n">legend_elements</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">Line2D</span><span class="p">([</span><span class="mi">0</span><span class="p">],</span> <span class="p">[</span><span class="mi">0</span><span class="p">],</span>  <span class="n">color</span><span class="o">=</span><span class="n">c</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">label</span><span class="o">=</span><span class="n">keys</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">markersize</span><span class="o">=</span><span class="mi">15</span><span class="p">))</span>

<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">handles</span><span class="o">=</span><span class="n">legend_elements</span><span class="p">,</span> <span class="n">title</span><span class="o">=</span><span class="s1">'Banner'</span><span class="p">,</span> <span class="n">bbox_to_anchor</span><span class="o">=</span><span class="p">(</span><span class="mf">1.05</span><span class="p">,</span> <span class="mi">1</span><span class="p">),</span> <span class="n">loc</span><span class="o">=</span><span class="s1">'upper left'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="263.63625pt" version="1.1" viewBox="0 0 474.185313 263.63625" width="474.185313pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:31.931734</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">func</span><span class="p">(</span><span class="n">pct</span><span class="p">):</span>
    <span class="k">return</span> <span class="s2">"</span><span class="si">{:.1f}</span><span class="s2">%"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">pct</span><span class="p">)</span>

<span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Permanent'</span><span class="p">]),</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]),</span>
                <span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Weapon'</span><span class="p">]),</span><span class="nb">len</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Novice'</span><span class="p">])])</span>

<span class="n">l</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"Permanent"</span><span class="p">,</span> <span class="s2">"Event"</span><span class="p">,</span> <span class="s2">"Weapon"</span><span class="p">,</span><span class="s2">"Novice"</span><span class="p">]</span>
<span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">y</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">l</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="k">lambda</span> <span class="n">pct</span><span class="p">:</span> <span class="n">func</span><span class="p">(</span><span class="n">pct</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="231.84pt" version="1.1" viewBox="0 0 264.60006 231.84" width="264.60006pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:32.357234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [16]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">makeList</span><span class="p">(</span><span class="n">lst</span><span class="p">,</span><span class="n">label</span><span class="p">,</span><span class="n">idx</span><span class="p">):</span>
    <span class="n">temp</span> <span class="o">=</span> <span class="p">[</span><span class="n">idx</span><span class="p">,</span><span class="n">label</span><span class="p">]</span>
    <span class="n">lst</span><span class="o">.</span><span class="n">index</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">MultiIndex</span><span class="o">.</span><span class="n">from_tuples</span><span class="p">([(</span><span class="n">ix</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="nb">str</span><span class="p">(</span><span class="n">ix</span><span class="p">[</span><span class="mi">1</span><span class="p">]))</span> <span class="k">for</span> <span class="n">ix</span> <span class="ow">in</span> <span class="n">lst</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">tolist</span><span class="p">()])</span>
    <span class="k">try</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">lst</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">][(</span><span class="s1">'Weapon'</span><span class="p">,</span><span class="s1">'3'</span><span class="p">)])</span>
    <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>

    <span class="k">try</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">lst</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">][(</span><span class="s1">'Weapon'</span><span class="p">,</span><span class="s1">'4'</span><span class="p">)])</span>
    <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>

    <span class="k">try</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">lst</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">][(</span><span class="s1">'Weapon'</span><span class="p">,</span><span class="s1">'5'</span><span class="p">)])</span>
    <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>

    <span class="k">try</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">lst</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">][(</span><span class="s1">'Character'</span><span class="p">,</span><span class="s1">'4'</span><span class="p">)])</span>
    <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>

    <span class="k">try</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">lst</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">][(</span><span class="s1">'Character'</span><span class="p">,</span><span class="s1">'5'</span><span class="p">)])</span>
    <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
        <span class="n">temp</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">temp</span>

<span class="k">def</span> <span class="nf">plotPie</span><span class="p">(</span><span class="n">e</span><span class="p">,</span><span class="n">title</span><span class="p">,</span><span class="n">i</span><span class="p">):</span>
    <span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">e</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span><span class="n">e</span><span class="p">[</span><span class="mi">3</span><span class="p">],</span><span class="n">e</span><span class="p">[</span><span class="mi">4</span><span class="p">],</span><span class="n">e</span><span class="p">[</span><span class="mi">5</span><span class="p">],</span><span class="n">e</span><span class="p">[</span><span class="mi">6</span><span class="p">]])</span>
    <span class="n">l</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"3*Weapon"</span><span class="p">,</span> <span class="s2">"4*Weapon"</span><span class="p">,</span> <span class="s2">"5*Weapon"</span><span class="p">,</span><span class="s2">"4*Character"</span><span class="p">,</span><span class="s2">"5*Character"</span><span class="p">]</span>
    <span class="n">l</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">l</span><span class="p">)[</span><span class="n">y</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
    <span class="n">y</span> <span class="o">=</span> <span class="n">y</span><span class="p">[</span><span class="n">y</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
    <span class="n">c</span><span class="o">=</span><span class="p">[]</span>
    <span class="k">for</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">l</span><span class="p">:</span>
        <span class="n">c</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">colors</span><span class="p">[</span><span class="n">v</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">num</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
    <span class="n">subtitle_string</span> <span class="o">=</span> <span class="n">title</span>
    <span class="k">for</span> <span class="n">v</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="nb">len</span><span class="p">(</span><span class="n">l</span><span class="p">)):</span>
        <span class="n">subtitle_string</span> <span class="o">=</span> <span class="n">subtitle_string</span> <span class="o">+</span> <span class="sa">f</span><span class="s2">"</span><span class="si">{</span><span class="n">l</span><span class="p">[</span><span class="n">v</span><span class="p">]</span><span class="si">}</span><span class="s2">:</span> <span class="si">{</span><span class="n">y</span><span class="p">[</span><span class="n">v</span><span class="p">]</span><span class="si">}</span><span class="se">\n</span><span class="s2">"</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="n">subtitle_string</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">pie</span><span class="p">(</span><span class="n">y</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">l</span><span class="p">,</span> <span class="n">autopct</span><span class="o">=</span><span class="k">lambda</span> <span class="n">pct</span><span class="p">:</span> <span class="n">func</span><span class="p">(</span><span class="n">pct</span><span class="p">),</span><span class="n">colors</span><span class="o">=</span><span class="n">c</span><span class="p">)</span>
<span class="n">colors</span> <span class="o">=</span> <span class="p">{}</span>
<span class="n">colors</span><span class="p">[</span><span class="s1">'3*Weapon'</span><span class="p">]</span><span class="o">=</span><span class="s1">'#424b96'</span>
<span class="n">colors</span><span class="p">[</span><span class="s1">'4*Weapon'</span><span class="p">]</span><span class="o">=</span><span class="s1">'#e87be8'</span>
<span class="n">colors</span><span class="p">[</span><span class="s1">'5*Weapon'</span><span class="p">]</span><span class="o">=</span><span class="s1">'#ffff00'</span>
<span class="n">colors</span><span class="p">[</span><span class="s1">'4*Character'</span><span class="p">]</span><span class="o">=</span><span class="s1">'#9908c2'</span>
<span class="n">colors</span><span class="p">[</span><span class="s1">'5*Character'</span><span class="p">]</span><span class="o">=</span><span class="s1">'#facc00'</span>
<span class="k">for</span> <span class="n">x</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">22</span><span class="p">):</span>
    <span class="n">curr</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">x</span><span class="p">]</span>
    <span class="n">event</span> <span class="o">=</span> <span class="n">curr</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Type'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">])</span><span class="o">.</span><span class="n">count</span><span class="p">()[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">.</span><span class="n">to_frame</span><span class="p">()</span>
    <span class="n">weapon</span> <span class="o">=</span> <span class="n">curr</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Weapon'</span><span class="p">]</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Type'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">])</span><span class="o">.</span><span class="n">count</span><span class="p">()[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">.</span><span class="n">to_frame</span><span class="p">()</span>
    <span class="n">perm</span> <span class="o">=</span> <span class="n">curr</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Permanent'</span><span class="p">]</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Type'</span><span class="p">,</span><span class="s1">'Rarity'</span><span class="p">])</span><span class="o">.</span><span class="n">count</span><span class="p">()[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">.</span><span class="n">to_frame</span><span class="p">()</span>
    <span class="n">novice</span> <span class="o">=</span> <span class="n">curr</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Novice'</span><span class="p">]</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Type'</span><span class="p">,</span> <span class="s1">'Rarity'</span><span class="p">])</span><span class="o">.</span><span class="n">count</span><span class="p">()[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">.</span><span class="n">to_frame</span><span class="p">()</span>
    <span class="n">counter</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">'ID'</span><span class="p">,</span><span class="s1">'Banner'</span><span class="p">,</span><span class="s1">'3* Weapon'</span><span class="p">,</span><span class="s1">'4* Weapon'</span><span class="p">,</span><span class="s1">'5* Weapon'</span><span class="p">,</span><span class="s1">'4* Unit'</span><span class="p">,</span><span class="s1">'5* Unit'</span><span class="p">])</span>    
    <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">30</span><span class="p">,</span><span class="mi">10</span><span class="p">))</span>
    <span class="n">num</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">if</span> <span class="n">event</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">num</span><span class="o">=</span><span class="n">num</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">weapon</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">num</span><span class="o">=</span><span class="n">num</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">perm</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">num</span><span class="o">=</span><span class="n">num</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">novice</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">num</span><span class="o">=</span><span class="n">num</span><span class="o">+</span><span class="mi">1</span>
    <span class="n">i</span><span class="o">=</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">event</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">e</span> <span class="o">=</span> <span class="n">makeList</span><span class="p">(</span><span class="n">event</span><span class="p">,</span><span class="s1">'event'</span><span class="p">,</span><span class="n">x</span><span class="p">)</span>
        <span class="n">plotPie</span><span class="p">(</span><span class="n">e</span><span class="p">,</span><span class="s1">'Event Banner</span><span class="se">\n</span><span class="s1">'</span><span class="p">,</span><span class="n">i</span><span class="p">)</span>
        <span class="n">i</span><span class="o">=</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span>

    <span class="k">if</span> <span class="n">weapon</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">e</span> <span class="o">=</span> <span class="n">makeList</span><span class="p">(</span><span class="n">weapon</span><span class="p">,</span><span class="s1">'Weapon'</span><span class="p">,</span><span class="n">x</span><span class="p">)</span>
        <span class="n">plotPie</span><span class="p">(</span><span class="n">e</span><span class="p">,</span><span class="s1">'Weapon Banner</span><span class="se">\n</span><span class="s1">'</span><span class="p">,</span><span class="n">i</span><span class="p">)</span>
        <span class="n">i</span><span class="o">=</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">perm</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">e</span> <span class="o">=</span> <span class="n">makeList</span><span class="p">(</span><span class="n">perm</span><span class="p">,</span><span class="s1">'Permanent'</span><span class="p">,</span><span class="n">x</span><span class="p">)</span>
        <span class="n">plotPie</span><span class="p">(</span><span class="n">e</span><span class="p">,</span><span class="s1">'Permanent Banner</span><span class="se">\n</span><span class="s1">'</span><span class="p">,</span><span class="n">i</span><span class="p">)</span>
        <span class="n">i</span><span class="o">=</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span>
    <span class="k">if</span> <span class="n">novice</span><span class="o">.</span><span class="n">empty</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
        <span class="n">e</span> <span class="o">=</span> <span class="n">makeList</span><span class="p">(</span><span class="n">novice</span><span class="p">,</span><span class="s1">'Novice'</span><span class="p">,</span><span class="n">x</span><span class="p">)</span>
        <span class="n">plotPie</span><span class="p">(</span><span class="n">e</span><span class="p">,</span><span class="s1">'Event Banner</span><span class="se">\n</span><span class="s1">'</span><span class="p">,</span><span class="n">i</span><span class="p">)</span>
        <span class="n">i</span><span class="o">=</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">suptitle</span><span class="p">(</span><span class="sa">f</span><span class="s1">'ID:</span> <span class="si">{</span><span class="n">x</span><span class="si">}</span> <span class="s1">'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span> 
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="604.376471pt" version="1.1" viewBox="0 0 1709.271213 604.376471" width="1709.271213pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:32.571735</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1736.622101 540.156522" width="1736.622101pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:33.011237</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1725.165445 540.156522" width="1725.165445pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:33.525235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1724.161262 540.156522" width="1724.161262pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:34.003234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1710.276878 540.156522" width="1710.276878pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:34.439735</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1736.143923 540.156522" width="1736.143923pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:34.897234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1709.599442 540.156522" width="1709.599442pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:35.485238</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1733.21246 540.156522" width="1733.21246pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:35.948235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1739.244622 540.156522" width="1739.244622pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:36.443735</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="604.376471pt" version="1.1" viewBox="0 0 1696.627328 604.376471" width="1696.627328pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:36.895735</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1736.82005 540.156522" width="1736.82005pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:37.328235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1731.666189 540.156522" width="1731.666189pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:37.823234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1738.182207 540.156522" width="1738.182207pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:38.322235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1710.572791 540.156522" width="1710.572791pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:38.913734</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1722.109843 540.156522" width="1722.109843pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:39.353234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="604.376471pt" version="1.1" viewBox="0 0 1709.183907 604.376471" width="1709.183907pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:39.768239</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1735.975275 540.156522" width="1735.975275pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:40.172234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1724.52988 540.156522" width="1724.52988pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:40.649234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="604.376471pt" version="1.1" viewBox="0 0 1708.98874 604.376471" width="1708.98874pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:41.062234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1725.289592 540.156522" width="1725.289592pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:41.463734</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="540.156522pt" version="1.1" viewBox="0 0 1730.467789 540.156522" width="1730.467789pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:41.915234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

is it actually 50/50 (Noraml distribution of 50/50) Isa c6 keqing resonable? Does money cause higher 5 star rate <- can get research on claimed rates cuz chinese <- linear regression #5 _= m_(rolls) + b Chance of getting weapon u want on weapon weapon (chance of getting featured weapon, and then chance of getting featured weapon you want)

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [17]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">plotHeat</span><span class="p">(</span><span class="n">item</span><span class="p">):</span>
    <span class="n">counts</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">banners</span><span class="p">:</span>
        <span class="n">r</span> <span class="o">=</span> <span class="p">[]</span>
        <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="n">items</span><span class="p">:</span>
            <span class="n">temp</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="n">j</span><span class="p">]</span>
            <span class="n">count</span> <span class="o">=</span> <span class="mi">0</span>
            <span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">temp</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
                <span class="k">if</span> <span class="n">charbanners</span><span class="p">[</span><span class="n">i</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span><span class="o"><=</span><span class="n">row</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span> <span class="ow">and</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span><span class="o"><=</span><span class="n">charbanners</span><span class="p">[</span><span class="n">i</span><span class="p">][</span><span class="mi">1</span><span class="p">]:</span>
                    <span class="n">count</span><span class="o">+=</span><span class="mi">1</span>
            <span class="n">r</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">count</span><span class="p">)</span>
        <span class="k">if</span> <span class="nb">sum</span><span class="p">(</span><span class="n">r</span><span class="p">)</span><span class="o">!=</span><span class="mi">0</span><span class="p">:</span>
            <span class="n">r</span> <span class="o">=</span> <span class="p">[</span><span class="n">t</span> <span class="o">/</span> <span class="nb">sum</span><span class="p">(</span><span class="n">r</span><span class="p">)</span> <span class="k">for</span> <span class="n">t</span> <span class="ow">in</span> <span class="n">r</span><span class="p">]</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">r</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="n">counts</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">r</span><span class="p">)</span>

    <span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s1">'figure.figsize'</span><span class="p">:(</span><span class="mi">30</span><span class="p">,</span><span class="mi">10</span><span class="p">)})</span>
    <span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span><span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
    <span class="n">g</span> <span class="o">=</span> <span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">counts</span><span class="p">,</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span><span class="n">cmap</span><span class="o">=</span><span class="s2">"YlGnBu"</span><span class="p">)</span>

    <span class="n">ax</span><span class="o">.</span><span class="n">xaxis</span><span class="o">.</span><span class="n">set_major_formatter</span><span class="p">(</span><span class="n">ticker</span><span class="o">.</span><span class="n">NullFormatter</span><span class="p">())</span>

    <span class="n">locs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">()</span> 
    <span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="o">.</span><span class="mi">5</span><span class="p">,</span><span class="nb">len</span><span class="p">(</span><span class="n">items</span><span class="p">)),</span> <span class="nb">tuple</span><span class="p">(</span><span class="n">items</span><span class="p">),</span><span class="n">rotation</span><span class="o">=</span><span class="mi">45</span><span class="p">,</span> <span class="n">horizontalalignment</span><span class="o">=</span><span class="s1">'right'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">yticks</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="o">.</span><span class="mi">5</span><span class="p">,</span><span class="nb">len</span><span class="p">(</span><span class="n">banners</span><span class="p">)),</span> <span class="nb">tuple</span><span class="p">(</span><span class="n">banners</span><span class="p">),</span><span class="n">rotation</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">horizontalalignment</span><span class="o">=</span><span class="s1">'right'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'Item'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'Banner'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [18]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span> <span class="n">items</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">3</span><span class="p">][</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
 <span class="n">banners</span> <span class="o">=</span> <span class="n">charbanners</span><span class="o">.</span><span class="n">keys</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">plotHeat</span><span class="p">(</span><span class="n">items</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="705.531485pt" version="1.1" viewBox="0 0 1559.617813 705.531485" width="1559.617813pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:51.431235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [20]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">items</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">4</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Weapon'</span><span class="p">][</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
<span class="n">items</span> <span class="o">=</span> <span class="n">items</span><span class="o">+</span><span class="nb">list</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">4</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Character'</span><span class="p">][</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
<span class="n">plotHeat</span><span class="p">(</span><span class="n">items</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="665.228076pt" version="1.1" viewBox="0 0 1559.617813 665.228076" width="1559.617813pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:55.335734</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">items</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">5</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Character'</span><span class="p">][</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
<span class="n">plotHeat</span><span class="p">(</span><span class="n">items</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="623.009914pt" version="1.1" viewBox="0 0 1553.500781 623.009914" width="1553.500781pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:58.117234</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

Is Banner

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">event_chars</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Tartaglia'</span><span class="p">,</span><span class="s1">'Ganyu'</span><span class="p">,</span><span class="s1">'Xiao'</span><span class="p">,</span><span class="s1">'Zhongli'</span><span class="p">,</span><span class="s1">'Albedo'</span><span class="p">,</span><span class="s1">'Venti'</span><span class="p">,</span><span class="s1">'Hu Tao'</span><span class="p">,</span><span class="s1">'Klee'</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">fiftyfifty</span> <span class="o">=</span> <span class="p">{}</span>

<span class="k">for</span> <span class="n">x</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">22</span><span class="p">):</span>
    <span class="n">diff</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">curr</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">x</span><span class="p">]</span>
    <span class="n">event</span> <span class="o">=</span> <span class="n">curr</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Type'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Character'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">curr</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">5</span><span class="p">]</span>
    <span class="n">skip</span> <span class="o">=</span> <span class="kc">False</span>
    <span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">event</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
        <span class="k">if</span> <span class="n">skip</span> <span class="ow">is</span> <span class="kc">False</span> <span class="ow">and</span> <span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span> <span class="ow">in</span> <span class="n">event_chars</span> <span class="ow">or</span> <span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Keqing'</span> <span class="ow">and</span> <span class="n">charbanners</span><span class="p">[</span><span class="s1">'Keqing'</span><span class="p">][</span><span class="mi">1</span><span class="p">]</span><span class="o">>=</span><span class="n">row</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span> <span class="ow">and</span> <span class="n">charbanners</span><span class="p">[</span><span class="s1">'Keqing'</span><span class="p">][</span><span class="mi">0</span><span class="p">]</span><span class="o"><=</span><span class="n">row</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">])):</span>
            <span class="n">diff</span><span class="o">+=</span><span class="mi">1</span>
            <span class="n">skip</span> <span class="o">=</span> <span class="kc">False</span>
        <span class="k">elif</span> <span class="n">skip</span> <span class="ow">is</span> <span class="kc">False</span><span class="p">:</span>
           <span class="n">diff</span><span class="o">-=</span><span class="mi">1</span>
           <span class="n">skip</span> <span class="o">=</span> <span class="kc">True</span>
    <span class="k">if</span> <span class="n">diff</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">fiftyfifty</span><span class="p">:</span>
        <span class="n">fiftyfifty</span><span class="p">[</span><span class="n">diff</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">fiftyfifty</span><span class="p">[</span><span class="n">diff</span><span class="p">]</span><span class="o">+=</span><span class="mi">1</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span><span class="mi">10</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">fiftyfifty</span><span class="o">.</span><span class="n">keys</span><span class="p">()),</span> <span class="n">fiftyfifty</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Fifty Fifty (Wins - Loss)"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedSVG jp-OutputArea-output " data-mime-type="image/svg+xml"><svg height="592.295469pt" version="1.1" viewBox="0 0 588.017031 592.295469" width="588.017031pt" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><metadata><rdf:rdf xmlns:cc="http://creativecommons.org/ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"><cc:work><dc:date>2021-05-10T22:34:59.153235</dc:date> <dc:format>image/svg+xml</dc:format> <dc:creator><cc:agent><dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title></cc:agent> </dc:creator></cc:work></rdf:rdf></metadata><defs><style type="text/css">*{stroke-linecap:butt;stroke-linejoin:round;}</style></defs></svg></div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [25]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">countBanner</span><span class="p">(</span><span class="n">df</span><span class="p">):</span>
    <span class="n">count</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">total</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">df</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
        <span class="k">if</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">!=</span><span class="mi">5</span><span class="p">:</span>
            <span class="n">count</span><span class="o">+=</span><span class="mi">1</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">total</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">count</span><span class="p">)</span>
            <span class="n">count</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">return</span> <span class="n">total</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [26]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">avgRate</span> <span class="o">=</span> <span class="p">{}</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">22</span><span class="p">):</span>
    <span class="n">temp</span> <span class="o">=</span> <span class="n">countBanner</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Event'</span><span class="p">])</span>
    <span class="n">temp</span> <span class="o">+=</span> <span class="n">countBanner</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Weapon'</span><span class="p">])</span>
    <span class="n">temp</span> <span class="o">+=</span> <span class="n">countBanner</span><span class="p">(</span><span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span> <span class="o">==</span><span class="s1">'Permanent'</span><span class="p">])</span>
    <span class="n">tot</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()[</span><span class="s1">'Id'</span><span class="p">]</span>
    <span class="n">avgRate</span><span class="p">[</span><span class="n">tot</span><span class="p">]</span> <span class="o">=</span> <span class="nb">sum</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span><span class="o">/</span><span class="nb">len</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [27]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">avgRate</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>
<span class="n">temp</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">avgRate</span><span class="o">.</span><span class="n">keys</span><span class="p">())</span>
<span class="n">x</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">temp</span><span class="p">:</span>
    <span class="n">x</span><span class="o">.</span><span class="n">append</span><span class="p">([</span><span class="n">i</span><span class="o">-</span><span class="mi">671</span><span class="p">])</span>
<span class="n">reg</span> <span class="o">=</span> <span class="n">LinearRegression</span><span class="p">()</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Number of Rolls per 5* =</span> <span class="si">{</span><span class="n">reg</span><span class="o">.</span><span class="n">intercept_</span><span class="si">}</span> <span class="s2">+</span> <span class="si">{</span><span class="n">reg</span><span class="o">.</span><span class="n">coef_</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span><span class="si">}</span><span class="s2">*Number of rolls Additional Rolls"</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">

<pre>Number of Rolls per 5* = 58.88330822061567 + -0.00028967894488069335*Number of rolls Additional Rolls
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [28]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="k">def</span> <span class="nf">checkProb</span><span class="p">():</span>
    <span class="n">num4</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">num5</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="n">cur_pity4</span> <span class="o">=</span> <span class="mi">9</span>
    <span class="n">cur_pity5</span> <span class="o">=</span> <span class="mi">89</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">10000</span><span class="p">):</span>
        <span class="n">rand</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">random</span><span class="p">()</span>
        <span class="k">if</span> <span class="n">rand</span> <span class="o"><</span> <span class="o">.</span><span class="mi">006</span> <span class="ow">or</span> <span class="n">cur_pity5</span> <span class="o"><=</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">num5</span> <span class="o">+=</span> <span class="mi">1</span>
            <span class="n">cur_pity4</span> <span class="o">=</span> <span class="mi">9</span>
            <span class="n">cur_pity5</span> <span class="o">=</span> <span class="mi">89</span>
        <span class="k">elif</span> <span class="n">rand</span> <span class="o"><</span> <span class="mf">0.051</span> <span class="ow">or</span> <span class="n">cur_pity4</span> <span class="o"><=</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">num4</span> <span class="o">+=</span> <span class="mi">1</span>
            <span class="n">cur_pity4</span> <span class="o">=</span> <span class="mi">9</span>
            <span class="n">cur_pity5</span> <span class="o">-=</span> <span class="mi">1</span>
        <span class="k">else</span><span class="p">:</span>
            <span class="n">cur_pity4</span> <span class="o">-=</span> <span class="mi">1</span>
            <span class="n">cur_pity5</span> <span class="o">-=</span> <span class="mi">1</span>
    <span class="k">return</span> <span class="p">((</span><span class="n">num4</span> <span class="o">/</span> <span class="mi">10000000</span> <span class="o">*</span> <span class="mi">100</span><span class="p">),</span> <span class="p">(</span><span class="n">num5</span> <span class="o">/</span> <span class="mi">10000000</span> <span class="o">*</span> <span class="mi">100</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">probs5</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">probs4</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">x</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">50</span><span class="p">):</span>
    <span class="n">temp</span> <span class="o">=</span> <span class="n">checkProb</span><span class="p">()</span>
    <span class="n">probs5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">temp</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span>
    <span class="n">probs4</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">temp</span><span class="p">[</span><span class="mi">1</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">probs5</span><span class="p">)</span><span class="o">/</span><span class="nb">len</span><span class="p">(</span><span class="n">probs5</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">probs4</span><span class="p">)</span><span class="o">/</span><span class="nb">len</span><span class="p">(</span><span class="n">probs4</span><span class="p">))</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

To preface, this is not fully related to the question of how fair the game is, but more of a personal question of how unlucky/lucky I am. Getting a five star is considered very lucky. However, Keqing, one of the five stars, is considered the worst five star. Therefore, by getting seven Keqings, is very polarized luck. This scenario is exactly what happened to me. The following code is a rudimentary analysis of what the chance of this was in my case. The code underneath starts by loading all the five star rolls from each banner as one if it is a Keqing or zero if it is anything else.

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">Image</span><span class="p">(</span><span class="n">filename</span><span class="o">=</span><span class="s1">'Character_Keqing_Card.jpg'</span><span class="p">,</span><span class="n">width</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span><span class="n">height</span><span class="o">=</span><span class="mi">50</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[19]:</div>

<div class="jp-RenderedImage jp-OutputArea-output jp-OutputArea-executeResult">![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/7QCcUGhvdG9zaG9wIDMuMAA4QklNBAQAAAAAAIAcAigAYkZCTUQwMTAwMGFhNTAxMDAwMDNhN2IwMDAwY2IyNzAxMDAzMDM2MDEwMDZhNWEwMTAwMjczNzAyMDBjMDM3MDMwMGU1NGYwMzAwOGI2NzAzMDAzNjkwMDMwMDQ3MWMwNTAwHAJnABRURjRMZkRxYVVrNWNvS1VuMzgyb//bAEMABQMEBAQDBQQEBAUFBQYHDAgHBwcHDwsLCQwRDxISEQ8RERMWHBcTFBoVEREYIRgaHR0fHx8TFyIkIh4kHB4fHv/bAEMBBQUFBwYHDggIDh4UERQeHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHh4eHv/AABEIA8ACHAMBIgACEQEDEQH/xAAfAAABBQEBAQEBAQAAAAAAAAAAAQIDBAUGBwgJCgv/xAC1EAACAQMDAgQDBQUEBAAAAX0BAgMABBEFEiExQQYTUWEHInEUMoGRoQgjQrHBFVLR8CQzYnKCCQoWFxgZGiUmJygpKjQ1Njc4OTpDREVGR0hJSlNUVVZXWFlaY2RlZmdoaWpzdHV2d3h5eoOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4eLj5OXm5+jp6vHy8/T19vf4+fr/xAAfAQADAQEBAQEBAQEBAAAAAAAAAQIDBAUGBwgJCgv/xAC1EQACAQIEBAMEBwUEBAABAncAAQIDEQQFITEGEkFRB2FxEyIygQgUQpGhscEJIzNS8BVictEKFiQ04SXxFxgZGiYnKCkqNTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqCg4SFhoeIiYqSk5SVlpeYmZqio6Slpqeoqaqys7S1tre4ubrCw8TFxsfIycrS09TV1tfY2dri4+Tl5ufo6ery8/T19vf4+fr/2gAMAwEAAhEDEQA/APq5f9Way9TmUXHkywebGFDEgfMvvWov+rNZF9dfY9RaVoyytEBXYzdE1na4uhdpOZY3UgE9a0j/AKwVmWbBL0xx5EUsYkC+hrTP+sFCAF++aan3Xpy/fNNT7r0xMP8AlnSn7gpP+WdKfuCgAPVa3E+6PpWGeq1uL90VhW6ESFooorEgKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigDK1H/Xt+FQH7y1PqP+vb8KgP3lrqhsax2E/wCWn4UL1aj/AJafhQvVqsYL/qzR/wAszQv+rNH/ACzNAIg1KUw2DyKASoHUcdazBDHeKYoy1rMfmMZ+63vV/WgTpcm0ZOB/OqEt0l3AZEUxzW4Vg3r2IpDWxr26lFRD1VQDSnqaIW3hW9VBoPU0yRy/6s1mawzwqsphWaMjG1hnafWtNf8AVmqWo3pgRYYo/Mmf7q44pFIg0iOaSV7ucEFhtUYxx/hWqf8AWCqNhJljHJN5s+Nz46L7Crx/1goQAv3zTU+69OX75pqfdemJh/yzpT9wUn/LOlP3BQAN/DW4v3RWG38Nbi/dFYVuhExaKKKxICiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACioLy7tbOBri7uIbeFfvSSuEUfieKo6D4j0LXTcDRtXstQNuwWb7PMH2E9M4os9wNWvJv2hvHreEU8P29nMwupNQjup0RsE28R+YH2YnH4Gtb4qeJPiDosUn/CKeEItSgCf8ffneYynHP7gYY4+pr5J8U61rOv65PqOvXU1xfsdrmRdpTH8IX+ED0xXZhcPzvmewH3lp91b31lDeWsqy288ayROp4ZWGQfyNT18m/BHxt8SrNV0bw5pT+IdOhOPs8qEJAD2EvAQexyPavqTQbjULnS4Z9V09NPvGGZbdZxMEOf74ABrGtRdJ2bAvUViaX4u8MapdSWmn6/pl1cRsUaKO6QtkdRjPP4Vt1k01uAUUUUgCiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAMrUf9e34VAfvLU+o/wCvb8KgP3lrqhsax2E/5afhQvVqP+Wn4UL1arGC/wCrNH/LM0L/AKs0f8szQCI7pXe2Kxttcjg1hM891MttHbrECw8zavX61vzyLFCZHOFUZNZX2x5pRPK3kWwPAH3pDSY0a0ahCFHQACkPU05Tl8joRTT1NMljl/1ZqhfO0ky2kR2Erukk7hfar6/6s1j6k6w3zebkRTRBCw7UmUiW0SCLUyluRt8r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
)</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [37]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">vincent</span> <span class="o">=</span> <span class="n">rolls</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">rolls</span><span class="p">[</span><span class="s1">'Id'</span><span class="p">]</span><span class="o">==</span><span class="mi">6</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [38]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">event</span> <span class="o">=</span> <span class="n">vincent</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Event'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">5</span><span class="p">]</span>
<span class="n">perm</span> <span class="o">=</span> <span class="n">vincent</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Permanent'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">5</span><span class="p">]</span>
<span class="n">novice</span> <span class="o">=</span> <span class="n">vincent</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Novice'</span><span class="p">]</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Rarity'</span><span class="p">]</span><span class="o">==</span><span class="mi">5</span><span class="p">]</span>
<span class="n">fiveChar</span> <span class="o">=</span> <span class="mi">5</span>
<span class="n">fiveWeap</span> <span class="o">=</span> <span class="mi">10</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [44]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">e5</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">event</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
    <span class="k">if</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Keqing'</span><span class="p">:</span>
        <span class="n">e5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">e5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">p5</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">perm</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
    <span class="k">if</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Keqing'</span><span class="p">:</span>
        <span class="n">p5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">p5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">n5</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">index</span><span class="p">,</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">novice</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
    <span class="k">if</span> <span class="n">row</span><span class="p">[</span><span class="s1">'Item'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Keqing'</span><span class="p">:</span>
        <span class="n">n5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">n5</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [45]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">e5</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[45]:</div>

<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">

<pre>[0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

In this case, the first roll is a fifty fifty for the banner character, but it was won so afterwards, it is another fifty fifty. This time I lost the fifty fift so there is a one fifth chance of getting Keqing. This leads to .5 _(.5_.2) = .05\. This means there was a five percent chance for the intial two rolls to happen.

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [46]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">p5</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[46]:</div>

<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">

<pre>[0, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1, 0, 0]</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

The permanent banner follows a similar style, but there are no fifty fifties and there are 15 possible five stars. Tehrefore by getting five Keqings from this banner from eleven five stars, the chance is: 14/15 ^ 6 * 1/15^5 = .00008704895%. This value is already super low, but thats not the last banner that needs to be accounted for.

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [49]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">vincent</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">vincent</span><span class="p">[</span><span class="s1">'Banner'</span><span class="p">]</span><span class="o">==</span><span class="s1">'Novice'</span><span class="p">]</span>
</pre>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-outputWrapper">

<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[49]:</div>

<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">

<div><style scoped="">.dataframe tbody tr th:only-of-type { vertical-align: middle; } .dataframe tbody tr th { vertical-align: top; } .dataframe thead th { text-align: right; }</style>

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>Id</th>

<th>Banner</th>

<th>Item</th>

<th>Type</th>

<th>Rarity</th>

<th>Date</th>

</tr>

</thead>

<tbody>

<tr>

<th>4278</th>

<td>6</td>

<td>Novice</td>

<td>Magic Guide</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4279</th>

<td>6</td>

<td>Novice</td>

<td>Emerald Orb</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4280</th>

<td>6</td>

<td>Novice</td>

<td>Bloodtainted Greatsword</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4281</th>

<td>6</td>

<td>Novice</td>

<td>Magic Guide</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4282</th>

<td>6</td>

<td>Novice</td>

<td>Slingshot</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4283</th>

<td>6</td>

<td>Novice</td>

<td>Cool Steel</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4284</th>

<td>6</td>

<td>Novice</td>

<td>Keqing</td>

<td>Character</td>

<td>5</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4285</th>

<td>6</td>

<td>Novice</td>

<td>Noelle</td>

<td>Character</td>

<td>4</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4286</th>

<td>6</td>

<td>Novice</td>

<td>Magic Guide</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4287</th>

<td>6</td>

<td>Novice</td>

<td>Harbinger of Dawn</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 18:41:28</td>

</tr>

<tr>

<th>4288</th>

<td>6</td>

<td>Novice</td>

<td>Thrilling Tales of Dragon Slayers</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4289</th>

<td>6</td>

<td>Novice</td>

<td>Cool Steel</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4290</th>

<td>6</td>

<td>Novice</td>

<td>Black Tassel</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4291</th>

<td>6</td>

<td>Novice</td>

<td>Sharpshooter's Oath</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4292</th>

<td>6</td>

<td>Novice</td>

<td>Slingshot</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4293</th>

<td>6</td>

<td>Novice</td>

<td>Magic Guide</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4294</th>

<td>6</td>

<td>Novice</td>

<td>Raven Bow</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4295</th>

<td>6</td>

<td>Novice</td>

<td>Beidou</td>

<td>Character</td>

<td>4</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4296</th>

<td>6</td>

<td>Novice</td>

<td>Bloodtainted Greatsword</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

<tr>

<th>4297</th>

<td>6</td>

<td>Novice</td>

<td>Emerald Orb</td>

<td>Weapon</td>

<td>3</td>

<td>2020-09-28 19:43:36</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

I got Keqing as my seventh roll on the novice banner. This only allows for five different five stars to be rooled so the calculation is as follows: (.94)^6 _.06_.2 = .82784%

</div>

</div>

<div class="jp-Cell-inputWrapper">

<div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">

This leads to the combining all these together .0082784 x .05 x .0000008704895 = 3.6031464e-10 = .0000000036031464% = 1/27,753,688,800\. Though this is the chance of my specific scenario, the highest chance of getting seven Keqings is still very low. The highest chance of getting all seven Keqings from the event banner would be (.5*.2)^7 = 1.0e-7\. For the permanent banner it would be (1/15)^7 = 5.85e-9\. To put these numbers to scale the chance of being struck by lightning is 1/114195, the chance of being attacked by a shark is 1/3748067, and the chance of winning the Powerball jackpot is 1/292,000,000\. My initial calculation is roughly a hundred times less likely to occur than winning the lottery. So what does all this mean? It means I am extremely lucky but in the worst way possible.

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="o">.</span><span class="mi">0082784</span><span class="o">*.</span><span class="mi">05</span><span class="o">*.</span><span class="mi">0000008704895</span> <span class="o">=</span> <span class="mf">3.6031464e-10</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">

<div class="jp-Cell-inputWrapper">

<div class="jp-InputArea jp-Cell-inputArea">

<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>

<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">

<div class="CodeMirror cm-s-jupyter">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="n">Sources</span><span class="p">:</span>
<span class="n">https</span><span class="p">:</span><span class="o">//</span><span class="n">www</span><span class="o">.</span><span class="n">sheknows</span><span class="o">.</span><span class="n">com</span><span class="o">/</span><span class="n">living</span><span class="o">/</span><span class="n">articles</span><span class="o">/</span><span class="mi">1023453</span><span class="o">/</span><span class="n">what</span><span class="o">-</span><span class="n">are</span><span class="o">-</span><span class="n">the</span><span class="o">-</span><span class="n">odds</span><span class="o">-</span><span class="mi">21</span><span class="o">-</span><span class="n">statistics</span><span class="o">-</span><span class="n">that</span><span class="o">-</span><span class="n">will</span><span class="o">-</span><span class="n">surprise</span><span class="o">-</span><span class="n">you</span><span class="o">/</span>
<span class="n">https</span><span class="p">:</span><span class="o">//</span><span class="n">www</span><span class="o">.</span><span class="n">base64</span><span class="o">-</span><span class="n">image</span><span class="o">.</span><span class="n">de</span><span class="o">/</span>
<span class="n">https</span><span class="p">:</span><span class="o">//</span><span class="n">genshin</span><span class="o">-</span><span class="n">impact</span><span class="o">.</span><span class="n">fandom</span><span class="o">.</span><span class="n">com</span><span class="o">/</span><span class="n">wiki</span><span class="o">/</span><span class="n">Keqing</span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>
=======
Readme
320
>>>>>>> 1a906e677b5d5c354e8e3293d5c2b0d97913120a
