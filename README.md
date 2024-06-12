<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Model-comparisons-with-audio-examples">Model comparisons with audio examples<a class="anchor-link" href="#Model-comparisons-with-audio-examples">¶</a></h4><p>Here we compare selected audio examples for the scenarios: matched DNS with no reverberation, mismatched VoiceBank+DEMAND training to DNS with no reverberation testing, and mismatched DNS training to VoiceBank+DEMAND testing.</p>
<p>We selected two examples for speech-like noise, specifically babble noise with a male and a female target speaker, and two non-speech noise types from the DNS test set. From the VoiceBank+DEMAND corpus, we chose a male speaker with musical noise and a female speaker with babble noise. Our aim was to choose files with a noisy mixture SNR of approximately 5 dB. However, the selection of non-speech noise examples was constrained by the inherent randomness of the noise distribution within our test sets, specifically for the VoiceBank+DEMAND corpus.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [25]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">IPython.display</span> <span class="kn">import</span> <span class="n">Image</span><span class="p">,</span> <span class="n">display</span><span class="p">,</span> <span class="n">HTML</span><span class="p">,</span> <span class="n">Audio</span>

<span class="k">def</span> <span class="nf">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">):</span>
    <span class="c1"># Titles for the audio files and image</span>
    <span class="n">audio_title_1</span> <span class="o">=</span> <span class="s1">'De-noised audio'</span>
    <span class="n">audio_title_2</span> <span class="o">=</span> <span class="s1">'Noisy audio'</span>
    <span class="n">audio_title_3</span> <span class="o">=</span> <span class="s1">'Clean audio'</span>

    <span class="n">image_width</span> <span class="o">=</span> <span class="s2">"1200px"</span>
    <span class="n">image_height</span> <span class="o">=</span> <span class="s2">"auto"</span>
    <span class="c1"># Create HTML to display the image and audio files in a column with titles</span>
    <span class="n">html_content</span> <span class="o">=</span> <span class="sa">f</span><span class="s2">"""</span>
<span class="s2">    &lt;div style="display: flex;"&gt;</span>
<span class="s2">        &lt;div style="margin-right: 20px;"&gt;</span>
<span class="s2">            &lt;div style="margin-top: 100px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_1</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">denoised_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">            &lt;div style="margin-top: 50px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_2</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">noisy_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">            &lt;div style="margin-top: 50px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_3</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">clean_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">        &lt;/div&gt;</span>
<span class="s2">        &lt;div&gt;</span>
<span class="s2">            &lt;p style="font-size: 24px;"&gt;</span><span class="si">{</span><span class="n">image_title</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">            &lt;img src="</span><span class="si">{</span><span class="n">image_path</span><span class="si">}</span><span class="s2">" alt="Image" style="width: </span><span class="si">{</span><span class="n">image_width</span><span class="si">}</span><span class="s2">; height: </span><span class="si">{</span><span class="n">image_height</span><span class="si">}</span><span class="s2">;"&gt;</span>
<span class="s2">        &lt;/div&gt;</span>
<span class="s2">    &lt;/div&gt;</span>
<span class="s2">    """</span>

    <span class="c1"># Display the audio files using HTML</span>
    <span class="n">display</span><span class="p">(</span><span class="n">HTML</span><span class="p">(</span><span class="n">html_content</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Comparing-CU-Net-with-the-CVU-Net-for-Magnitude/Phase-features-in-the-matched-DNS-no-reverberation-scenario">Comparing CU-Net with the CVU-Net for Magnitude/Phase features in the matched DNS-no reverberation scenario<a class="anchor-link" href="#Comparing-CU-Net-with-the-CVU-Net-for-Magnitude/Phase-features-in-the-matched-DNS-no-reverberation-scenario">¶</a></h4><p>Three different audio files are chosen for this comparison. One male and one female speaker scenarios with babble noise and one female speaker with non-stationary noise (wind).</p>
</div>
</div>
</div>
</div><div class='jp-Cell jp-CodeCell jp-Notebook-cell celltag_{ "tags": [ "hide_input" ] }'>
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [26]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Wind noise</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_170.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_170.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on wind noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_170.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_170.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on wind noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Vacuum noise female speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_175.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_175.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_175.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Babble male speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_255.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_255.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on babble noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_255.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_255.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Babble Female speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_147.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_147.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on babble noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_147.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_147.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/cvunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>
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
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on wind noise with a male speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_170.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cvunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on wind noise with a male speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_170.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_175.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cvunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_175.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on babble noise with a male speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_255.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cvunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a male speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_255.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on babble noise with a female speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cunet-maph/cunet-maph_fileid_147.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/cvunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a female speaker</p>
<img alt="Image" src="audio_examples/dns-norev/cvunet-maph/cvunet-maph_fileid_147.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Now-we-look-at-the-exact-same-files,-but-for-the-mismatched-scenario-when-the-models-are-trained-on-VoiceBank+DEMAND-instead">Now we look at the exact same files, but for the mismatched scenario when the models are trained on VoiceBank+DEMAND instead<a class="anchor-link" href="#Now-we-look-at-the-exact-same-files,-but-for-the-mismatched-scenario-when-the-models-are-trained-on-VoiceBank+DEMAND-instead">¶</a></h4><p>It is important to note that we use the (Ma/Ph)-model variations primarily because for the sake of comparison here. Listening to the (Re/Im)-variations might improve the listening experience since those models exhibit a slightly larger SDR differences, making these differences somewhat easier to detect by listening. For instance, the first comparison below reveals an SDR difference of 0.85 dB for (Ma/Ph), compared to 0.96 dB for (Re/Im), both favoring the CVU-Net. For another comparison on (Re/Im)-models, the files and figures are also included in this repository.</p>
</div>
</div>
</div>
</div><div class='jp-Cell jp-CodeCell jp-Notebook-cell celltag_{ "tags": [ "hide_input" ] }'>
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [27]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Wind noise</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_170.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_170.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on wind noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_170.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on wind noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Vacuum noise female speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_175.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_175.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_175.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Babble male speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_255.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_255.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on babble noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_255.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a male speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Babble Female speaker</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_147.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-norev/noisy_fileid_147.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CU-Net (Ma/Ph) de-noising on babble noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_147.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/voice-dns-norev/cvunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a female speaker"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>
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
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on wind noise with a male speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_170.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cvunet-maph/clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp205_wind_407027_1_snr1_tl-24_fileid_170.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on wind noise with a male speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_170.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_175.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cvunet-maph/clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp257_vacuum_273194_2_snr4_tl-18_fileid_175.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising a vacuum cleaner noise with a female speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_175.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on babble noise with a male speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_255.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cvunet-maph/clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp50_babble_188218_24_snr4_tl-29_fileid_255.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a male speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_255.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CU-Net (Ma/Ph) de-noising on babble noise with a female speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cunet-maph/cunet-maph_fileid_147.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 100px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/cvunet-maph/clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-norev/noisy_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 50px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/voice-dns-norev/clean_clnsp25_babble_188218_21_snr5_tl-25_fileid_147.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">Example of the CVU-Net (Ma/Ph) de-noising on babble noise with a female speaker</p>
<img alt="Image" src="audio_examples/voice-dns-norev/cvunet-maph/cvunet-maph_fileid_147.png" style="width: 1200px; height: auto;"/>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Training-on-the-DNS-dataset-and-evaluating-on-VoiceBank+DEMAND">Training on the DNS dataset and evaluating on VoiceBank+DEMAND<a class="anchor-link" href="#Training-on-the-DNS-dataset-and-evaluating-on-VoiceBank+DEMAND">¶</a></h4>
</div>
</div>
</div>
</div><div class='jp-Cell jp-CodeCell jp-Notebook-cell celltag_{ "tags": [ "hide_input" ] }'>
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [30]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">):</span>
    <span class="c1"># Titles for the audio files and image</span>
    <span class="n">audio_title_1</span> <span class="o">=</span> <span class="s1">'De-noised audio'</span>
    <span class="n">audio_title_2</span> <span class="o">=</span> <span class="s1">'Noisy audio'</span>
    <span class="n">audio_title_3</span> <span class="o">=</span> <span class="s1">'Clean audio'</span>
    <span class="n">image_width</span> <span class="o">=</span> <span class="s2">"860px"</span>
    <span class="n">image_height</span> <span class="o">=</span> <span class="s2">"auto"</span>
    <span class="c1"># Create HTML to display the image and audio files in a column with titles</span>
    <span class="n">html_content</span> <span class="o">=</span> <span class="sa">f</span><span class="s2">"""</span>
<span class="s2">    &lt;div style="display: flex;"&gt;</span>
<span class="s2">        &lt;div style="margin-right: 20px;"&gt;</span>
<span class="s2">            &lt;div style="margin-top: 150px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_1</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">denoised_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">            &lt;div style="margin-top: 150px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_2</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">noisy_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">            &lt;div style="margin-top: 100px;"&gt;</span>
<span class="s2">                &lt;p&gt;</span><span class="si">{</span><span class="n">audio_title_3</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">                &lt;audio controls&gt;</span>
<span class="s2">                    &lt;source src="</span><span class="si">{</span><span class="n">clean_path</span><span class="si">}</span><span class="s2">" type="audio/mpeg"&gt;</span>
<span class="s2">                    Your browser does not support the audio element.</span>
<span class="s2">                &lt;/audio&gt;</span>
<span class="s2">            &lt;/div&gt;</span>
<span class="s2">        &lt;/div&gt;</span>
<span class="s2">        &lt;div&gt;</span>
<span class="s2">            &lt;p style="font-size: 24px;"&gt;</span><span class="si">{</span><span class="n">image_title</span><span class="si">}</span><span class="s2">&lt;/p&gt;</span>
<span class="s2">            &lt;img src="</span><span class="si">{</span><span class="n">image_path</span><span class="si">}</span><span class="s2">" alt="Image" style="width: </span><span class="si">{</span><span class="n">image_width</span><span class="si">}</span><span class="s2">; height: </span><span class="si">{</span><span class="n">image_height</span><span class="si">}</span><span class="s2">;"&gt;</span>
<span class="s2">        &lt;/div&gt;</span>
<span class="s2">    &lt;/div&gt;</span>
<span class="s2">    """</span>

    <span class="c1"># Display the audio files using HTML</span>
    <span class="n">display</span><span class="p">(</span><span class="n">HTML</span><span class="p">(</span><span class="n">html_content</span><span class="p">))</span>

<span class="c1"># Male speaker with music and rustling noise</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp232_160.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/clean_p232_160.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/noisy_p232_160.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/p232_160.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CU-Net (Ma/Ph) de-noising for male speaker with music &amp; background noise"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp232_160.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/clean_p232_160.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/noisy_p232_160.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/p232_160.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CVU-Net (Ma/Ph) for male speaker with music &amp; background noise"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Female Speaker with music</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp257_430.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/clean_p257_430.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/noisy_p257_430.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/p257_430.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CU-Net (Ma/Ph) de-noising for female speaker with music"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp257_430.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/p257_430.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CVU-Net (Ma/Ph) for female speaker with music noise"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># Female Speaker with babble</span>
<span class="c1"># CU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp257_411.png"</span>
<span class="n">clean_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/clean_p257_411.wav"</span>
<span class="n">noisy_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/noisy_p257_411.wav"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cunet-maph/p257_411.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CU-Net (Ma/Ph) de-noising for female speaker with babble noise"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>

<span class="c1"># CVU-Net</span>
<span class="n">image_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp257_411.png"</span>
<span class="n">denoised_path</span> <span class="o">=</span> <span class="s2">"audio_examples/dns-to-voice/cvunet-maph/p257_411.wav"</span>
<span class="n">image_title</span> <span class="o">=</span> <span class="s2">"CVU-Net (Ma/Ph) for female speaker with babble noise"</span>
<span class="n">create_html_display</span><span class="p">(</span><span class="n">image_path</span><span class="p">,</span> <span class="n">clean_path</span><span class="p">,</span> <span class="n">noisy_path</span><span class="p">,</span> <span class="n">denoised_path</span><span class="p">,</span> <span class="n">image_title</span><span class="p">)</span>
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
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cunet-maph/p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CU-Net (Ma/Ph) de-noising for male speaker with music &amp; background noise</p>
<img alt="Image" src="audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp232_160.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cvunet-maph/p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p232_160.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CVU-Net (Ma/Ph) for male speaker with music &amp; background noise</p>
<img alt="Image" src="audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp232_160.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cunet-maph/p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CU-Net (Ma/Ph) de-noising for female speaker with music</p>
<img alt="Image" src="audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp257_430.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cvunet-maph/p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p257_430.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CVU-Net (Ma/Ph) for female speaker with music noise</p>
<img alt="Image" src="audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp257_430.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cunet-maph/p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CU-Net (Ma/Ph) de-noising for female speaker with babble noise</p>
<img alt="Image" src="audio_examples/dns-to-voice/cunet-maph/cunet-maph_fileidp257_411.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output" data-mime-type="text/html" tabindex="0">
<div style="display: flex;">
<div style="margin-right: 20px;">
<div style="margin-top: 150px;">
<p>De-noised audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/cvunet-maph/p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 150px;">
<p>Noisy audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/noisy_p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
<div style="margin-top: 100px;">
<p>Clean audio</p>
<audio controls="">
<source src="audio_examples/dns-to-voice/clean_p257_411.wav" type="audio/mpeg"/>
                    Your browser does not support the audio element.
                </audio>
</div>
</div>
<div>
<p style="font-size: 24px;">CVU-Net (Ma/Ph) for female speaker with babble noise</p>
<img alt="Image" src="audio_examples/dns-to-voice/cvunet-maph/cvunet-maph_fileidp257_411.png" style="width: 860px; height: auto;"/>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
