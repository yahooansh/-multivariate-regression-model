# Multivariate-regression-model
 reviewing the Housing dataset and to create a multivariate regression model.
The dataset has 546 observations and 9 variables:
Independent Variables
Lotsize – measured in sq meters
Bedrooms - # of bedrooms
Bathrms - # of bathrooms
Stories - # of stories
GaragePl – # of Garage places
Recroom – Recreation Room Yes/No
Fullbase – Full basement Yes/No
Airco – Air-conditioning Yes/No

Dependent Variable
Price – in US dollars
![Screenshot 2024-10-26 130120](https://github.com/user-attachments/assets/795351e0-c55f-4bf7-a1f7-d2d1f8e48c14)
[Housing price presentation.pptx](https://github.com/user-attachments/files/17531399/Housing.price.presentation.pptx)
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"><html><head></head><body>















    




    
    
    
    

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[18]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Load Libraries</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">from</span> <span class="nn">statsmodels.stats.outliers_influence</span> <span class="kn">import</span> <span class="n">variance_inflation_factor</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[34]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Load Dataset</span>
<span class="n">data</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;./HousingDB.csv&#39;</span><span class="p">)</span>
<span class="n">data</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[34]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>price</th>
      <th>lotsize</th>
      <th>bedrooms</th>
      <th>bathrms</th>
      <th>stories</th>
      <th>garagepl</th>
      <th>recroom</th>
      <th>fullbase</th>
      <th>airco</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>42000.0</td>
      <td>5850</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>no</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38500.0</td>
      <td>4000</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>no</td>
      <td>no</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>49500.0</td>
      <td>3060</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>no</td>
      <td>no</td>
      <td>no</td>
    </tr>
    <tr>
      <th>3</th>
      <td>60500.0</td>
      <td>6650</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>yes</td>
      <td>no</td>
      <td>no</td>
    </tr>
    <tr>
      <th>4</th>
      <td>61000.0</td>
      <td>6360</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>no</td>
      <td>no</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[35]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Create One Hot Encoded Dataframe</span>

<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">OneHotEncoder</span>

<span class="n">ohe</span> <span class="o">=</span> <span class="n">OneHotEncoder</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="s1">&#39;first&#39;</span><span class="p">)</span>

<span class="n">data_object</span> <span class="o">=</span> <span class="n">data</span><span class="o">.</span><span class="n">select_dtypes</span><span class="p">(</span><span class="s1">&#39;object&#39;</span><span class="p">)</span>
<span class="n">ohe</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">data_object</span><span class="p">)</span>

<span class="n">codes</span> <span class="o">=</span> <span class="n">ohe</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">data_object</span><span class="p">)</span><span class="o">.</span><span class="n">toarray</span><span class="p">()</span>
<span class="n">feature_names</span> <span class="o">=</span> <span class="n">ohe</span><span class="o">.</span><span class="n">get_feature_names_out</span><span class="p">(</span><span class="n">data_object</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>

<span class="n">data_ohe</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">data</span><span class="o">.</span><span class="n">select_dtypes</span><span class="p">(</span><span class="n">exclude</span><span class="o">=</span><span class="s1">&#39;object&#39;</span><span class="p">),</span> 
               <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">codes</span><span class="p">,</span><span class="n">columns</span><span class="o">=</span><span class="n">feature_names</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="n">data_ohe</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[35]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>price</th>
      <th>lotsize</th>
      <th>bedrooms</th>
      <th>bathrms</th>
      <th>stories</th>
      <th>garagepl</th>
      <th>recroom_yes</th>
      <th>fullbase_yes</th>
      <th>airco_yes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>42000.0</td>
      <td>5850</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38500.0</td>
      <td>4000</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>49500.0</td>
      <td>3060</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>60500.0</td>
      <td>6650</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>61000.0</td>
      <td>6360</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[36]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Key Statistics</span>
<span class="n">data_ohe</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[36]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>price</th>
      <th>lotsize</th>
      <th>bedrooms</th>
      <th>bathrms</th>
      <th>stories</th>
      <th>garagepl</th>
      <th>recroom_yes</th>
      <th>fullbase_yes</th>
      <th>airco_yes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
      <td>546.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>68121.597070</td>
      <td>5150.265568</td>
      <td>2.965201</td>
      <td>1.285714</td>
      <td>1.807692</td>
      <td>0.692308</td>
      <td>0.177656</td>
      <td>0.349817</td>
      <td>0.316850</td>
    </tr>
    <tr>
      <th>std</th>
      <td>26702.670926</td>
      <td>2168.158725</td>
      <td>0.737388</td>
      <td>0.502158</td>
      <td>0.868203</td>
      <td>0.861307</td>
      <td>0.382573</td>
      <td>0.477349</td>
      <td>0.465675</td>
    </tr>
    <tr>
      <th>min</th>
      <td>25000.000000</td>
      <td>1650.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>49125.000000</td>
      <td>3600.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>62000.000000</td>
      <td>4600.000000</td>
      <td>3.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>82000.000000</td>
      <td>6360.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>190000.000000</td>
      <td>16200.000000</td>
      <td>6.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>3.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[37]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Correlation of features(independent variable) with output(predicting variable)</span>
<span class="n">cor</span> <span class="o">=</span> <span class="n">data_ohe</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span>
<span class="n">cor_target</span> <span class="o">=</span> <span class="nb">abs</span><span class="p">(</span><span class="n">cor</span><span class="p">[</span><span class="s1">&#39;price&#39;</span><span class="p">])</span>

<span class="c1">#Selecting highly correlated features</span>
<span class="n">relevant_features</span> <span class="o">=</span> <span class="n">cor_target</span><span class="p">[</span><span class="n">cor_target</span><span class="o">&gt;</span> <span class="o">-</span><span class="mf">0.10</span><span class="p">]</span>
<span class="n">relevant_features</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[37]:</div>




<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult">
<pre>price           1.000000
lotsize         0.535796
bathrms         0.516719
airco_yes       0.453347
stories         0.421190
garagepl        0.383302
bedrooms        0.366447
recroom_yes     0.254960
fullbase_yes    0.186218
Name: price, dtype: float64</pre>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[38]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Find Independent Column Correlations</span>
<span class="k">def</span> <span class="nf">correlation</span><span class="p">(</span><span class="n">dataset</span><span class="p">,</span><span class="n">threshold</span><span class="p">):</span>
    <span class="n">col_corr</span><span class="o">=</span> <span class="p">[]</span> <span class="c1"># List of correlated columns</span>
    <span class="n">corr_matrix</span><span class="o">=</span><span class="n">dataset</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span> <span class="c1">#finding correlation between columns</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span> <span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">corr_matrix</span><span class="o">.</span><span class="n">columns</span><span class="p">)):</span> <span class="c1">#Number of columns</span>
        <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span> <span class="p">(</span><span class="n">i</span><span class="p">):</span>
            <span class="k">if</span> <span class="nb">abs</span><span class="p">(</span><span class="n">corr_matrix</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="n">i</span><span class="p">,</span><span class="n">j</span><span class="p">])</span><span class="o">&gt;</span><span class="n">threshold</span><span class="p">:</span> <span class="c1">#checking correlation between columns</span>
                <span class="n">colName</span><span class="o">=</span><span class="p">(</span><span class="n">corr_matrix</span><span class="o">.</span><span class="n">columns</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">corr_matrix</span><span class="o">.</span><span class="n">columns</span><span class="p">[</span><span class="n">j</span><span class="p">])</span> <span class="c1">#getting correlated columns</span>
                <span class="n">col_corr</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">colName</span><span class="p">)</span> <span class="c1">#adding correlated column name</span>
    <span class="k">return</span> <span class="n">col_corr</span> <span class="c1">#returning set of column names</span>
<span class="n">col</span><span class="o">=</span><span class="n">correlation</span><span class="p">(</span><span class="n">data_ohe</span><span class="p">,</span><span class="mf">0.4</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Correlated columns @ 0.4:&#39;</span><span class="p">,</span> <span class="n">col</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Correlated columns @ 0.4: [(&#39;lotsize&#39;, &#39;price&#39;), (&#39;bathrms&#39;, &#39;price&#39;), (&#39;stories&#39;, &#39;price&#39;), (&#39;stories&#39;, &#39;bedrooms&#39;), (&#39;airco_yes&#39;, &#39;price&#39;)]
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[40]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Define x and y variable</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">data_ohe</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;price&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">data_ohe</span><span class="p">[</span><span class="s1">&#39;price&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>

<span class="c1">#Create Train and Test Datasets</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>
<span class="n">x_train</span><span class="p">,</span><span class="n">x_test</span><span class="p">,</span><span class="n">y_train</span><span class="p">,</span><span class="n">y_test</span><span class="o">=</span><span class="n">train_test_split</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">y</span><span class="p">,</span><span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>

<span class="c1">#Scale the Data</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>
<span class="n">sc</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span>
<span class="n">x_train2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x_train</span><span class="p">)</span>
<span class="n">x_test2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">x_test</span><span class="p">)</span>

<span class="c1">#Model</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LinearRegression</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[41]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Create Standard Model - using Dummy Variables</span>

<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">metrics</span>

<span class="k">for</span> <span class="n">name</span><span class="p">,</span><span class="n">method</span> <span class="ow">in</span> <span class="p">[(</span><span class="s1">&#39;Linear regression&#39;</span><span class="p">,</span> <span class="n">LinearRegression</span><span class="p">())]:</span> 
    <span class="n">method</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train2</span><span class="p">,</span><span class="n">y_train</span><span class="p">)</span>
    <span class="n">predict</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_test2</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1"> Regression Model - using OneHotEncoder&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Method: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">name</span><span class="p">))</span>   

<span class="c1">#Coefficents</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Intercept: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">float</span><span class="p">(</span><span class="n">method</span><span class="o">.</span><span class="n">intercept_</span><span class="p">)))</span>
<span class="n">coeff_table</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">method</span><span class="o">.</span><span class="n">coef_</span><span class="p">),</span>
                         <span class="n">data_ohe</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;price&#39;</span><span class="p">],</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">columns</span><span class="p">,</span>
                         <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;Coefficients&#39;</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="n">coeff_table</span><span class="p">)</span>
    
<span class="c1">#R2,MAE,MSE and RMSE</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">R2: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">metrics</span><span class="o">.</span><span class="n">r2_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">predict</span><span class="p">)))</span>
<span class="n">adjusted_r_squared</span> <span class="o">=</span> <span class="mi">1</span><span class="o">-</span><span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">metrics</span><span class="o">.</span><span class="n">r2_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">predict</span><span class="p">))</span><span class="o">*</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">y</span><span class="p">)</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">/</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">y</span><span class="p">)</span><span class="o">-</span><span class="n">x</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Adj_R2: </span><span class="si">{:0.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">adjusted_r_squared</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Mean Absolute Error: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">metrics</span><span class="o">.</span><span class="n">mean_absolute_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">predict</span><span class="p">)))</span>  
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Mean Squared Error: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">metrics</span><span class="o">.</span><span class="n">mean_squared_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">predict</span><span class="p">)))</span>  
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Root Mean Squared Error: </span><span class="si">{:.2f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">metrics</span><span class="o">.</span><span class="n">mean_squared_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">predict</span><span class="p">))))</span> 
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
 Regression Model - using OneHotEncoder

Method: Linear regression

Intercept: 68860.08
              Coefficients
lotsize        8634.475677
bedrooms       1368.299630
bathrms        7127.520695
stories        6567.390507
garagepl       4597.365623
recroom_yes    2054.126514
fullbase_yes   3661.398670
airco_yes      5736.782817

R2: 0.54
Adj_R2: 0.53
Mean Absolute Error: 12127.85
Mean Squared Error: 253496059.87
Root Mean Squared Error: 15921.56
</pre>
</div>
</div>

</div>

</div>

</div>









<script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/mathjax.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
						if (document.querySelector('math') || /\$\$|\\\(|\\\[|\\begin{|\\ref{|\\eqref{/.test(document.body.innerHTML)) {
							document.querySelectorAll('mspace[linebreak="newline"]').forEach(elm => {
								elm.setAttribute('style', 'display: block; height: 0.5rem;');
							});

							window.D2L.MathJax.loadMathJax({
								outputScale: 1.5,
								renderLatex: false,
								enableMML3Support: false
							});
						}
					});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/prism.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					document.querySelectorAll('.d2l-code').forEach(code => {
						window.D2L.Prism.formatCodeElement(code);
					});
				});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/embeds.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					window.D2L.EmbedRenderer.renderEmbeds(document.body);
				});</script></body></html>
