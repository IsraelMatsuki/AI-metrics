# Measuring the Progress of AI Research

This repository contains a [Jupyter Notebook](http://jupyter.org/), which you
can see live at [https://eff.org/ai/metrics](https://www.eff.org/ai/metrics).
It collects problems and metrics / datasets from the artificial intelligence
and machine learning research literature, and tracks progress on them. You can
use it to see how things are progressing in specific subfields or AI/ML as a
whole, as a place to report new results you've obtained, and as place to look
for problems that might benefit from having new datasets/metrics designed for
them, or as a source to build on for data science projects.

At EFF we're also interested in collecting this data to understand the likely
implications of AI, but to begin with we're focused on gathering it.

_Original authors: [Peter
Eckersley](https://www.eff.org/about/staff/peter-eckersley) and [Yomna
Nasser](https://ynasser.github.io/) at [EFF](https://eff.org)<br>_

With contributions from: [Gennie Gebhart](https://www.eff.org/about/staff/gennie-gebhart) and [Owain Evans](https://www.fhi.ox.ac.uk/team/owain-evans/)<br>
Inspired by and merging data from:

* Rodrigo Benenson's ["Who is the Best at X / Are we there yet?"](https://rodrigob.github.io/are_we_there_yet/build/#about) collating machine vision datasets & progress
* Jack Clark and Miles Brundage's [collection of AI progress measurements](https://raw.githubusercontent.com/AI-metrics/master_text/master/archive/AI-metrics-data.txt)
* Sarah Constantin's [Performance Trends in AI](https://srconstantin.wordpress.com/2017/01/28/performance-trends-in-ai/)
* Katja Grace's [Algorithmic Progress in Six Domains](https://intelligence.org/files/AlgorithmicProgress.pdf)
* The Swedish Computer Chess Association's [History of Computer Chess performance](https://en.wikipedia.org/wiki/Swedish_Chess_Computer_Association#Rating_list_year-end_leaders)
* Qi Wu _et al._'s [Visual Question Answering: A survey of Methods and Datasets](https://arxiv.org/abs/1607.05910)
* Eric Yuan's [Comparison of Machine Reading Comprehension Datasets](http://eric-yuan.me/compare-popular-mrc-datasets/)

## How to contribute to this notebook

This notebook is an open source, community effort. You can help by adding new metrics, data and problems to it! If you're feeling ambitious you can also improve its semantics or build new analyses into it. Here are some high level tips on how to do that.

### 1. If you're comfortable with git and Jupyter Notebooks, or are happy to learn

If you've already worked a lot with `git` and IPython/Jupyter Notebooks, here's a quick list of things you'll need to do:

1. Install [Jupyter Notebook](https://jupyter.readthedocs.io/en/latest/install.html) and [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
    * On an Ubuntu or Debian system, you can do: <br><pre>sudo apt-get install git
      sudo apt-get install ipython-notebook || sudo apt-get install jupyter-notebook || sudo apt-get install python-notebook</pre>
    * Make sure you have IPython Notebook version 3 or higher. If your OS
      doesn't provide it, you might need to enable backports, or use `pip` to
      install it.
2. Install this notebook's Python dependencies:<br>
    * On Ubuntu or Debian, do: <br><pre>    sudo apt-get install python-{cssselect,lxml,matplotlib{,-venn},numpy,requests,seaborn}</pre>
    * On other systems, use your native OS packages, or use `pip`: <br><pre>    pip install cssselect lxml matplotlib{,-venn} numpy requests seaborn</pre>
3. Fork our repo on
   github: https://github.com/AI-metrics/AI-metrics#fork-destination-box
4. [Clone](https://help.github.com/articles/cloning-a-repository/) the repo on your machine, and `cd` into the directory it's using
4. Configure your copy of git to use [IPython Notebook merge filters](http://pascalbugnion.net/blog/ipython-notebooks-and-git.html) to prevent conflicts when multiple people edit the Notebook simultaneously. You can do that with these two commands in the cloned repo:
    <pre>git config --file .gitconfig filter.clean_ipynb.clean $PWD/ipynb_drop_output</pre>
    <pre>git config --file .gitconfig filter.clean_ipynb.smudge cat</pre>
5. Run Jupyter Notebok in the project directory (the command may be `ipython notebook`, `jupyter notebook`, `jupyter-notebook`, or `python notebook` depending on your system), then go to [localhost:8888](http://localhost:8888) and edit the Notebook `AI-progress-metrics.ipynb` to your heart's content

6. Save and commit your work (`git commit -a -m "DESCRIPTION OF WHAT YOU CHANGED"`)
7. Push it to your remote repo
8. Send us a pull request!


### 2. If you want something very simple

Microsoft Azure has an IPython / Jupyter service that will let you run and modify notebooks from their servers. You can clone this Notebook and work with it via their service: https://notebooks.azure.com/EFForg/libraries/ai-progress. Unfortunately there are a few issues with running the notebook on Azure:

* arXiv seems to block requests from Azure's IP addresses, so it's impossible to automatically extract information about paper when running the Notebook there
* The Azure Notebooks service seems to transform Unicode characters in strange ways, creating extra work merging changes from that source


## Notes on importing data

* Each `.measure()` call is a data point of a specific algorithm on a specific metric/dataset. Thus one paper will often produce multiple measurements on multiple metrics. It's most important to enter results that were at or near the frontier of best performance on the date they were published, though this isn't a strict requirement and it's nice to have a sense of the performance of the field, or of algorithms that are otherwise notable even if they aren't the frontier for a specific problem.
* When multiple revisions of a paper (typically on arXiv) have the same results on some metric, use the date of the first version (the CBTest results in [this paper](https://arxiv.org/abs/1606.02245v4) are an example)
* When subsequent revisions of a paper improve on the original results ([example](https://arxiv.org/abs/1606.01549v3)), use the date and scores of the first results, or if each revision is interesting / on the frontier of best performance, include each paper
  * We didn't check this carefully for our first ~100 measurement data points :(. In order to denote when we've checked which revision of an arXiv preprint first published a result, cite the specific version (https://arxiv.org/abs/1606.01549v3 rather than https://arxiv.org/abs/1606.01549); that way we can see which previous entries should be double-checked for this form of inaccuracy.
* Where possible, use a clear short name or acronym for each algorithm. The full paper name can go in the `papername` field (and is auto-populated for some papers). When matplotlib 2.1 ships we may be able to get nice [rollovers](https://github.com/matplotlib/matplotlib/pull/5754) with metadata like this. Or perhaps we can switch to D3 to get that type of interactivity.



## What to work on

* If you know of ML datasets/metrics that aren't included yet, add them
* If there are papers with interesting results for metrics that aren't included, add them
* If you know of important problems that humans can solve, and machine learning systems may or may not yet be able to, and they're missing from our taxonomy, you can propose them
* Look at our [Github issue list](https://github.com/AI-metrics/master_text) perhaps starting with those tagged as [good volunteer tasks](https://github.com/AI-metrics/master_text/issues?q=is%3Aissue+is%3Aopen+label%3A%22Good+volunteer+task%22).
* You can also add missing conferences / journals to the venue-to-date mapping table (unhide the source code and search for `conference_dates`):


 
# FAQ
 
**Q: What's the point of this project? How does it tie in with the EFF's mission?**
 
Given that machine learning tools and AI techniques are increasingly part of our everyday lives, it is critical that journalists, policy makers, and technology users understand the state of the field. When improperly designed or deployed, machine learning methods can violate privacy, threaten safety, and perpetuate inequality and injustice. Stakeholders must be able to anticipate such risks and policy questions before they arise, rather than playing catch-up with the technology. To this end, it’s part of the responsibility of researchers, engineers, and developers in the field to help make information about their life-changing research widely available and understandable
 
 
**Q: Why haven't you included dataset X?**
 
There are a tiny number of us and this is a large task! If you'd like to add more data, please [send us a pull request](https://www.eff.org/ai/metrics#How-to-contribute-to-this-notebook)
 
 
**Q: Do you track other things besides how well-solved particular tasks are? For instance, the speed and efficiency of training?**
 
No, but we'd love to. If you are motivated to help organize that data, please [dive in and improve the notebook](https://www.eff.org/ai/metrics#How-to-contribute-to-this-notebook)!
 
 
**Q: Have you thought about how to visualise this data and make it more accessible?**
 
We've considered a variety of things, but decided that the iPython notebook was ultimately the most accessible for now. We're very open to suggestions about visualizations and accessibility, so feel free to [reach out](https://www.eff.org/ai/metrics#How-to-contribute-to-this-notebook) if you have any ideas!
 
Also, if you'd like to build visualizations on top of this project, all the data we use is available in the easily digestible JSON format in [`progress.json`](export-api/v01/progress.json). If you do so, let us know and we'll try to link to it.
 
 
**Q: Is this an EFF project?**
 
Yes, but we'd like it to grow to be a self-sustaining community effort supported by a coalition of organizations. EFF did the initial work of making the Notebook, but we built on several [excellent datasets collected by many other people](https://www.eff.org/files/ai-progress/AI-progress-metrics.html#Measuring-the-Progress-of-AI-Research), and had a number of productive collabrative discussions most especially with people at OpenAI and the Future of Humanity Institute in preparing the document. We will strive to keep the [authorship section](https://www.eff.org/files/ai-progress/AI-progress-metrics.html#Measuring-the-Progress-of-AI-Research) of the Notebook accurate as others continue to contribue.
 
 
**Q: When will artificial general intelligence happen?**
 
We don't know--and this project is not meant to answer this question. Instead, we’re interested in compiling data to guide evidence-based conversations about the state of the art in various corners of AI and machine learning research.
