# Latex



### 个人笔记

doucument 对应整个文档; section 对应章节段落, subsection 对应小节; section 创建的段落使用数字作为章节号,并且出现在目录中. paragraph 不适用数字标识,也不出现在目录中.

section - subsection - paragraph

* 公式

  ```text
  1、数学公式的前后要加上 $ 或 \( 和 \)，比如：$f(x) =3x +7$ 和 \(f(x) =3x +7\) 效果是一样的；
  如果用 \[ 和 \]，或者使用 $$和 $$，则该公式独占一行；
  如果用 \begin{equation} 和 \end{equation}，则公式除了独占一行还会自动被添加序号， 如何公式不想编号则使用 \begin{equation*} 和 \end{equation*}.
  ​
  2, 空心字母$\mathbb{S}$   需要的包\usepackage{amsfonts,amssymb}
  ```

  ​

### 伪代码模板

```text
% 完成任务再上传这个模板
```

效果如下:

### Elsevier 模板

```ruby
\documentclass[review]{elsarticle}
​
\usepackage{lineno,hyperref}
\modulolinenumbers[5]
​
\journal{Journal of \LaTeX\ Templates}
​
%%%%%%%%%%%%%%%%%%%%%%%
%% Elsevier bibliography styles
%%%%%%%%%%%%%%%%%%%%%%%
%% To change the style, put a % in front of the second line of the current style and
%% remove the % from the second line of the style you would like to use.
%%%%%%%%%%%%%%%%%%%%%%%
​
%% Numbered
%\bibliographystyle{model1-num-names}
​
%% Numbered without titles
%\bibliographystyle{model1a-num-names}
​
%% Harvard
%\bibliographystyle{model2-names.bst}\biboptions{authoryear}
​
%% Vancouver numbered
%\usepackage{numcompress}\bibliographystyle{model3-num-names}
​
%% Vancouver name/year
%\usepackage{numcompress}\bibliographystyle{model4-names}\biboptions{authoryear}
​
%% APA style
%\bibliographystyle{model5-names}\biboptions{authoryear}
​
%% AMA style
%\usepackage{numcompress}\bibliographystyle{model6-num-names}
​
%% `Elsevier LaTeX' style
\bibliographystyle{elsarticle-num}
%%%%%%%%%%%%%%%%%%%%%%%
​
\begin{document}
​
\begin{frontmatter}
%% 这里是开头标题
\title{Combine Double DQN with Actor-critic Method for Robot Navigation}
\tnotetext[mytitlenote]{Fully documented templates are available in the elsarticle package on \href{http://www.ctan.org/tex-archive/macros/latex/contrib/elsarticle}{CTAN}.}
​
%% Group authors per affiliation: 这里是作者信息,姓名,地址
\author{Menghao Wu\fnref{myfootnote}}
\address{Radarweg 29, Amsterdam}
\fntext[myfootnote]{Since 1880.}
​
%% or include affiliations in footnotes: 脚注下的机构名称
\author[mymainaddress,mysecondaryaddress]{Elsevier Inc}
\ead[url]{www.elsevier.com}
​
\author[mysecondaryaddress]{Global Customer Service\corref{mycorrespondingauthor}}
\cortext[mycorrespondingauthor]{Corresponding author}
\ead{support@elsevier.com}
​
\address[mymainaddress]{1600John F Kennedy Boulevard, Philadelphia}
\address[mysecondaryaddress]{360Park Avenue South, New York}
%% -------------------------- 下面是文章的开头 abstract---------------------------%%
\begin{abstract}
  Recently,reinforcement learning has been general used by lots field besides robot navigation. In this paper ,I introduce a new method called DoubleAC to deal with Robot navigation problem in Continuous control field.
\end{abstract}
​
\begin{keyword}
\textttQ-learning \sepReinforcement learning \sepRobot navigation
\MSC[2010]00-01\sep 99-00
\end{keyword}
​
\end{frontmatter}
​
\linenumbers
%% -------------------------- 下面是文章的开头 ---------------------------%%
\section{The Elsevier article class}
​
\paragraph{Introduction}
​
\paragraph{Installation}If the document class \emph{elsarticle}is not available on your computer, you can download and install the system package \emph{texlive-publishers}(Linux) or install the \LaTeX\ package \emph{elsarticle}using the package manager of your \TeX\ installation, which is typically \TeX\ Live or Mik\TeX.
​
\paragraph{Usage}Once the package is properly installed, you can use the document class \emph{elsarticle}to create a manuscript. Please make sure that your manuscript follows the guidelines in the Guide for Authors of the relevant journal. It is not necessary to typeset your manuscript in exactly the same way as an article, unless you are submitting to a camera-ready copy (CRC) journal.
​
\paragraph{Functionality}The Elsevier article class is based on the standard article class and supports almost all of the functionality of that class. In addition, it features commands and options to format the
\begin{itemize}
\itemdocument style
\itembaselineskip
\itemfront matter
\itemkeywords and MSC codes
\itemtheorems, definitions and proofs
\itemlables of enumerations
\itemcitation style and labeling.
\end{itemize}
​
\section{Front matter}
​
The author names and affiliations could be formatted in two ways:
\begin{enumerate}[(1)]
\itemGroup the authors per affiliation.
\itemUse footnotes to indicate the affiliations.
\end{enumerate}
See the front matter of this document for examples. You are recommended to conform your choice to the journal you are submitting to.
​
\section{Bibliography styles}
​
There are various bibliography styles available. You can select the style of your choice in the preamble of this document. These styles are Elsevier styles based on standard styles like Harvard and Vancouver. Please use Bib\TeX\ to generate your bibliography and include DOIs whenever available.
​
Here are two sample references: \cite{Feynman1963118,Dirac1953888}.
​
\section*{References}
​
\bibliography{library.bib}
​
\end{document}
```

