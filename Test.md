```tikz
%\documentstyle[10pt,twoside]{article}
\documentstyle[twoside, 11pt]{article}
\setlength{\oddsidemargin}{0.25 in}
\setlength{\evensidemargin}{-0.25 in}
\setlength{\topmargin}{-0.6 in}
\setlength{\textwidth}{6.5 in}
\setlength{\textheight}{8.5 in}
\setlength{\headsep}{0.75 in}
\setlength{\parindent}{0 in}
\setlength{\parskip}{0.1 in}

%
% The following commands sets up the lecnum (lecture number)
% counter and make various numbering schemes work relative
% to the lecture number.
%
\newcounter{lecnum}
\renewcommand{\thepage}{\thelecnum-\arabic{page}}
\renewcommand{\thesection}{\thelecnum.\arabic{section}}
\renewcommand{\theequation}{\thelecnum.\arabic{equation}}
\renewcommand{\thefigure}{\thelecnum.\arabic{figure}}
\renewcommand{\thetable}{\thelecnum.\arabic{table}}

%
% The following macro is used to generate the header.
%
\newcommand{\problemset}[3]{
   \pagestyle{myheadings}
   \thispagestyle{plain}
   \newpage
   \setcounter{lecnum}{#1}
   \setcounter{page}{1}
   \noindent
   \begin{center}
   \framebox{
      \vbox{\vspace{2mm}
    \hbox to 6.28in { {\bf CS~21~~~Decidability and Tractability
                        \hfill Winter 2023} }
       \vspace{4mm}
       \hbox to 6.28in { {\Large \hfill Problem Set #1  \hfill} }
       \vspace{2mm}
       \hbox to 6.28in { {\it Out: #2 \hfill Due: #3} }
      \vspace{2mm}}
   }
   \end{center}
   \vspace*{4mm}
}

%
% Convention for citations is authors' initials followed by the year.
% For example, to cite a paper by Leighton and Maggs you would type
% \cite{LM89}, and to cite a paper by Strassen you would type \cite{S69}.
% (To avoid bibliography problems, for now we redefine the \cite command.)
%
\renewcommand{\cite}[1]{[#1]}

\input{epsf}

%Use this command for a figure; it puts a figure in wherever you want it.
%usage: \fig{NUMBER}{FIGURE-SIZE}{CAPTION}{FILENAME}
\newcommand{\fig}[4]{
            \vspace{0.2 in}
            \setlength{\epsfxsize}{#2}
            \centerline{\epsfbox{#4}}
            \begin{center}
            Figure \thelecnum.#1:~#3
            \end{center}
    }

% Use these for theorems, lemmas, proofs, etc.
\newtheorem{theorem}{Theorem}[lecnum]
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem{claim}[theorem]{Claim}
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem{definition}[theorem]{Definition}
\newenvironment{proof}{{\bf Proof:}}{\hfill\rule{2mm}{2mm}}

% Some useful equation alignment commands, borrowed from TeX
\makeatletter
\def\eqalign#1{\,\vcenter{\openup\jot\m@th
  \ialign{\strut\hfil$\displaystyle{##}$&$\displaystyle{{}##}$\hfil
      \crcr#1\crcr}}\,}
\def\eqalignno#1{\displ@y \tabskip\@centering
  \halign to\displaywidth{\hfil$\displaystyle{##}$\tabskip\z@skip
    &$\displaystyle{{}##}$\hfil\tabskip\@centering
    &\llap{$##$}\tabskip\z@skip\crcr
    #1\crcr}}
\def\leqalignno#1{\displ@y \tabskip\@centering
  \halign to\displaywidth{\hfil$\displaystyle{##}$\tabskip\z@skip
    &$\displaystyle{{}##}$\hfil\tabskip\@centering
    &\kern-\displaywidth\rlap{$##$}\tabskip\displaywidth\crcr
    #1\crcr}}
\makeatother

% **** IF YOU WANT TO DEFINE ADDITIONAL MACROS FOR YOURSELF, PUT THEM HERE:


\begin{document}
\problemset{1}{January 11}{\bf {January 18}}

Reminder: you are encouraged to work in groups of two or three;
however you must turn in your own write-up and note with whom you
worked. You may consult the course notes and the text (Sipser). The
full honor code guidelines and collaboration policy can be found in the course syllabus.


Please attempt all problems. {\bf Please turn in your solutions via
  Gradescope, by 1pm on the due date.}

\begin{enumerate}
\item Let $f:\Sigma^* \rightarrow \Sigma^*$ be an arbitrary
function. You are asked to (1) define a related language $L_f
\subseteq \Gamma^*$, and (2) describe how a computer program could
use a procedure that decides $L_f$ to compute $f$, and vice-versa.
Here $\Gamma$ is an alphabet that may or may not be the same as
$\Sigma$. Ideally, on input $x$, your program should invoke the
procedure that decides $L_f$ at most polynomially many times in
the length of $x$ and the length of $f(x)$, (but attaining this
quantitative goal is not required to get full credit for this
problem).

This justifies our use of languages (or {\em decision problems})
rather than the more general notion of function problems.

\item This problem is based on Problem 1.38 (Problem 1.31 in the
First Edition), which defines a new kind of automaton: the {\em
all-paths-NFA}. An all-paths-NFA is defined by a 5-tuple $(Q,
\Sigma, \delta, q_0, F)$ just like an NFA. The only difference is
in the acceptance criterion. An all-paths-NFA accepts a string $x$
if {\em every} computation of M on $x$ ends in an accept state
(computations that ``die'' before reading to the end of the input
are not counted). For comparison, recall that an NFA accepts a
string $x$ if {\em some} computation of $M$ on $x$ ends in an
accept state. \label{prob:int}

\begin{enumerate}

\item Prove that $L$ is a regular language if and only if $L$ is
recognized by an all-paths-NFA.

\item Use part (a) to prove that the regular languages are closed
under intersection. That is, prove that if $A$ and $B$ are regular
languages, then
\[C = (A \cap B) = \{x : x \in A \mbox{ and } x \in B\}\]
is a regular language.

\item Let $M = (Q, \Sigma, \delta, q_0, F)$ be an NFA that
recognizes language $L$. Let $M_{\mbox{flip}} = (Q, \Sigma,
\delta, q_0, F')$ be the all-paths-NFA defined by taking $F' = Q -
F$, and let $L_{\mbox{flip}}$ be the language recognized by
$M_{\mbox{flip}}$. How are $L$ and $L_{\mbox{flip}}$ related?
Briefly justify your answer.
\end{enumerate}


\item A {\em palindrome} is a string that reads the same forwards
as backwards (ignoring spaces); an example is ``lonely tylenol''.
Let $\Sigma$ be the 26 letter English alphabet. Prove that the
language consisting of all palindromes is not regular.

\item A language over an alphabet $\Sigma$ with only one symbol is
still meaningful. It is called a unary language. In this problem
$\Sigma = \{0\}$.
\begin{enumerate}
\item For a positive integer $n$, define the language $L_n
\subseteq \Sigma^*$ to be the set of all strings whose length is
not divisible by $n$. Prove that for all $n \ge 1$, $L_n$ is a
regular language.

\item Prove that the language ${\sc primes} \subseteq \Sigma^*$,
consisting of all strings whose length is a prime number, is not
regular.
\end{enumerate}
Spend a few minutes to convince yourself that this does not
contradict Problem \ref{prob:int}(b), in which you proved that the
regular languages are closed under intersection. You do not need to
write down and turn in your thoughts (but you can if you wish). 
\end{enumerate}

\end{document}
```
