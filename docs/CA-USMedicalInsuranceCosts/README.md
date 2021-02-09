In this Codecademy exercise I was asked to explore U.S. Medical Insurance Cost data using Python. The document below was generated from Google Colaboratory, based on Jupyter Notebook, and shows the process I followed to examine my hypothesis that smoking plays the biggest role in increasing insurance costs on average. 

Please note that I am unsure of the data provenance since this was an educational exercise using realistic data. 

  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="U.S.-Medical-Insurance-Costs">U.S. Medical Insurance Costs<a class="anchor-link" href="#U.S.-Medical-Insurance-Costs">&#182;</a></h1><p>Given the available variables, my hypothesis is that smoking plays the biggest role in increasing insurance costs on average.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Get-the-data">Get the data<a class="anchor-link" href="#Get-the-data">&#182;</a></h1><p>Use the csv reader to get the data, split it up by row into an array of values per line. Also, store each column in its own variable.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">csv</span>
<span class="n">insuranceData</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">age</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">sex</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">bmi</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">children</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">smoker</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">region</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">charges</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="s1">&#39;/content/drive/MyDrive/Codecademy/US Medical Insurance Costs/insurance.csv&#39;</span><span class="p">,</span> <span class="n">newline</span><span class="o">=</span><span class="s1">&#39;&#39;</span><span class="p">)</span> <span class="k">as</span> <span class="n">csvfile</span><span class="p">:</span>
  <span class="n">reader</span> <span class="o">=</span> <span class="n">csv</span><span class="o">.</span><span class="n">DictReader</span><span class="p">(</span><span class="n">csvfile</span><span class="p">)</span>
  <span class="k">for</span> <span class="n">row</span> <span class="ow">in</span> <span class="n">reader</span><span class="p">:</span>
      <span class="n">insuranceData</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">)</span>
      <span class="c1">#print(row)</span>
      <span class="n">age</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;age&#39;</span><span class="p">])</span>
      <span class="n">sex</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;sex&#39;</span><span class="p">])</span>
      <span class="n">bmi</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;bmi&#39;</span><span class="p">])</span>
      <span class="n">children</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;children&#39;</span><span class="p">])</span>
      <span class="n">smoker</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;smoker&#39;</span><span class="p">])</span>
      <span class="n">region</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;region&#39;</span><span class="p">])</span>
      <span class="n">charges</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">float</span><span class="p">(</span><span class="n">row</span><span class="p">[</span><span class="s1">&#39;charges&#39;</span><span class="p">]))</span>
</pre></div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Define-analysis-functions.">Define analysis functions.<a class="anchor-link" href="#Define-analysis-functions.">&#182;</a></h1><p>Averaging is a function I plan to use a lot. I know there are optimizations that can be done on lists so I decided to keep it separate even though it looks simple.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">averageOfList</span><span class="p">(</span><span class="n">lst</span><span class="p">):</span>
  <span class="k">return</span> <span class="nb">sum</span><span class="p">(</span><span class="n">lst</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">lst</span><span class="p">)</span>
</pre></div>


</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Perform-Analysis">Perform Analysis<a class="anchor-link" href="#Perform-Analysis">&#182;</a></h1><p>What is the average charge for smokers versus non-smokers?</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">chargeVSmoke</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">smoker</span><span class="p">,</span><span class="n">charges</span><span class="p">))</span>
<span class="n">smokerChargeAverage</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">chargeVSmoke</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;yes&#39;</span><span class="p">])</span>
<span class="n">nonSmokerChargeAverage</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">chargeVSmoke</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;no&#39;</span><span class="p">])</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Smokers average charges: $</span><span class="si">{0:.2f}</span><span class="se">\n</span><span class="s1">Non Smokers Average Charges $</span><span class="si">{1:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">smokerChargeAverage</span><span class="p">,</span> <span class="n">nonSmokerChargeAverage</span><span class="p">))</span>
</pre></div>


</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

<pre><code>Smokers average charges: $32050.23
Non Smokers Average Charges $8434.27</code></pre>
<p>Smokers pay a lot more for thier coverage. For smokers and non-smokers, what is the gender makeup?</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sexVSmoke</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">sex</span><span class="p">,</span><span class="n">smoker</span><span class="p">))</span>
<span class="n">smokerSex</span> <span class="o">=</span> <span class="p">[</span><span class="n">sex</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span> <span class="ow">in</span> <span class="n">sexVSmoke</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;yes&#39;</span><span class="p">]</span>
<span class="n">nonSmokerSex</span> <span class="o">=</span> <span class="p">[</span><span class="n">sex</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span> <span class="ow">in</span> <span class="n">sexVSmoke</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;no&#39;</span><span class="p">]</span>

<span class="n">smokerSexMalePercent</span> <span class="o">=</span> <span class="nb">sum</span><span class="p">(</span><span class="mi">1</span> <span class="k">for</span> <span class="n">sex</span> <span class="ow">in</span> <span class="n">smokerSex</span> <span class="k">if</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;male&#39;</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">smokerSex</span><span class="p">)</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">smokerSexFemalePercent</span> <span class="o">=</span> <span class="nb">sum</span><span class="p">(</span><span class="mi">1</span> <span class="k">for</span> <span class="n">sex</span> <span class="ow">in</span> <span class="n">smokerSex</span> <span class="k">if</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;female&#39;</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">smokerSex</span><span class="p">)</span> <span class="o">*</span> <span class="mi">100</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;There are </span><span class="si">{:.2f}</span><span class="s1">% Males and </span><span class="si">{:.2f}% F</span><span class="s1">emales who smoke in our dataset.&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">smokerSexMalePercent</span><span class="p">,</span> <span class="n">smokerSexFemalePercent</span><span class="p">))</span>

<span class="n">nonSmokerSexMalePercent</span> <span class="o">=</span> <span class="nb">sum</span><span class="p">(</span><span class="mi">1</span> <span class="k">for</span> <span class="n">sex</span> <span class="ow">in</span> <span class="n">nonSmokerSex</span> <span class="k">if</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;male&#39;</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">nonSmokerSex</span><span class="p">)</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">nonSmokerSexFemalePercent</span> <span class="o">=</span> <span class="nb">sum</span><span class="p">(</span><span class="mi">1</span> <span class="k">for</span> <span class="n">sex</span> <span class="ow">in</span> <span class="n">nonSmokerSex</span> <span class="k">if</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;female&#39;</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">nonSmokerSex</span><span class="p">)</span> <span class="o">*</span> <span class="mi">100</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;There are </span><span class="si">{:.2f}</span><span class="s1">% Males and </span><span class="si">{:.2f}% F</span><span class="s1">emales who don</span><span class="se">\&#39;</span><span class="s1">t smoke in our dataset.&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">nonSmokerSexMalePercent</span><span class="p">,</span> <span class="n">nonSmokerSexFemalePercent</span><span class="p">))</span>
</pre></div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

<pre><code>There are 58.03% Males and 41.97% Females who smoke in our dataset.
There are 48.59% Males and 51.41% Females who don't smoke in our dataset.</code></pre>
<p>It seems like there are more male smokers than females and roughly equal sexes for non-smokers. Do the Males and Females in the smoker/non-smoker category pay similar amounts?</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sexVSmokeVCharge</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">sex</span><span class="p">,</span> <span class="n">smoker</span><span class="p">,</span> <span class="n">charges</span><span class="p">))</span>

<span class="n">smokerMaleChargeAvg</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">sexVSmokeVCharge</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;yes&#39;</span> <span class="ow">and</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;male&#39;</span><span class="p">])</span>
<span class="n">smokerFemaleChargeAvg</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">sexVSmokeVCharge</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;yes&#39;</span> <span class="ow">and</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;female&#39;</span><span class="p">])</span>

<span class="n">nonSmokerMaleChargeAvg</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">sexVSmokeVCharge</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;no&#39;</span> <span class="ow">and</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;male&#39;</span><span class="p">])</span>
<span class="n">nonSmokerFemaleChargeAvg</span> <span class="o">=</span> <span class="n">averageOfList</span><span class="p">([</span><span class="n">charge</span> <span class="k">for</span> <span class="n">sex</span><span class="p">,</span> <span class="n">smoke</span><span class="p">,</span> <span class="n">charge</span> <span class="ow">in</span> <span class="n">sexVSmokeVCharge</span> <span class="k">if</span> <span class="n">smoke</span> <span class="o">==</span> <span class="s1">&#39;no&#39;</span> <span class="ow">and</span> <span class="n">sex</span> <span class="o">==</span> <span class="s1">&#39;female&#39;</span><span class="p">])</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Smoker males are charged $</span><span class="si">{:.2f}</span><span class="se">\n</span><span class="s1">Smoker females are charged $</span><span class="si">{:.2f}</span><span class="se">\n</span><span class="s1">Non-smoker males are charged $</span><span class="si">{:.2f}</span><span class="se">\n</span><span class="s1">Non-smoker females are charged $</span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">smokerMaleChargeAvg</span><span class="p">,</span> <span class="n">smokerFemaleChargeAvg</span><span class="p">,</span> <span class="n">nonSmokerMaleChargeAvg</span><span class="p">,</span> <span class="n">nonSmokerFemaleChargeAvg</span><span class="p">))</span>
</pre></div>


</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div><div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

<pre><code>Smoker males are charged $33042.01
Smoker females are charged $30679.00
Non-smoker males are charged $8087.20
Non-smoker females are charged $8762.30</code></pre>
<p>Interestingly males pay more if they smoke than females, but females who don't smoke pay more than males who don't smoke. Smokers still pay the most on average.</p>
<hr>
<p>During my initial scan of data I did note that there are a few people who pay significantly more who don't smoke.</p>
<p>A 60 year-old female with a bmi of 25.84, no children, non-smoker in the northwest pays <code>$28923.13692</code>.</p>
<p>A 33 year-old male with a bmi of 22.705, no children, non-smoker, in the northwest pays <code>$21984.47061</code>.</p>
<p>While these seem out of line with the norm they pay significantly less still than smokers.</p>

</div>
</div>
</div>
    </div>
  </div>


