# Resume

### LaTex resume remplate

https://github.com/treyhunner/resume

#### resume.cls

```latex
% resume.cls

% \documentstyle{resume}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Copyright (C) 2010 by Trey Hunner
%
% Copying and distribution of this file, with or without modification,
% are permitted in any medium without royalty provided the copyright
% notice and this notice are preserved.  This file is offered as-is,
% without any warranty.
%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\ProvidesClass{resume}[2010/07/10 v0.9 Resume class]

\LoadClass[11pt,letterpaper]{article}

\usepackage[parfill]{parskip}       % Do not indent paragraphs
\usepackage{array}                  % required for boldface tabular columns
\usepackage{ifthen}

\nofiles                            % .aux files are not needed for resumes
\pagestyle{empty}                   % resumes do not need page numbers

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% HEADINGS: Commands for printing name and address

\def \name#1{\def\@name{#1}}        % \name command can be used to set name
\def \@name {}                      % Set \@name to empty by default

\def \addressSep {$\diamond$}         % Set default address seperator

% One or two address lines can be specified 
\let \@addressone \relax
\let \@addresstwo \relax

% \address command can be used to set first and second address (optional)
\def \address #1{
  \@ifundefined{@addresstwo}{
    \def \@addresstwo {#1}
  }{
    \def \@addressone {#1}
  }
}

% \printaddress is used to style an address line (given as input)
\def \printaddress #1{
  \begingroup
    \def \\ {\addressSep\ }
    \centerline{#1}
  \endgroup
  \par
  \addressskip
}

% \printname is used to print the name as a page header
\def \printname {
  \begingroup
    \centerline{\textbf{\MakeUppercase{\namesize\@name}}}
  \endgroup
  \par
  \nameskip
}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% DOCUMENT: Create the head of the document

\AtBeginDocument{                     % Begin document
  \printname                        % Print the name specified with \name
  \@ifundefined{@addressone}{}{     % Print the first address if specified
    \printaddress{\@addressone}}
  \@ifundefined{@addresstwo}{}{     % Print the second address if specified
    \printaddress{\@addresstwo}}
}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% SECTIONS: Create section headings

% Used to create large resume section
\newenvironment{rSection}[1]{
  \sectionskip
  \textbf{\MakeUppercase{#1}}
  \sectionlineskip
  \hrule
  \begin{list}{}{
    \setlength{\leftmargin}{1.5em}
  }
  \item[]
}{
  \end{list}
}

% Used to format job listing
\newenvironment{rSubsection}[4]{
  %%%%%%%%%%%%%%%%%%%%%% Default Layout: %%%%%%%%%%%%%%%%%%%%%%%%
  %%    Employer (bold)                     Dates (regular)    %%
  %%    Title (emphasis)                Location (emphasis)    %%
  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
  \textbf{#1}                 \hfill                  {    #2}% Stop a space
  \ifthenelse{\equal{#3}{}}{}{
  \\
  \emph{#3}                \hfill                  \emph{#4}% Stop a space
  }\smallskip
  % \cdot used for bullets, items non-indented
  \begin{list}{$\cdot$}{\leftmargin=0em}
  \itemsep -0.5em \vspace{-0.5em}
}{
  \end{list}
  \vspace{0.5em}
}

\def\namesize{\huge}
\def\nameskip{\medskip}
\def\addressskip{\smallskip}
\def\sectionskip{\bigskip}
\def\sectionlineskip{\medskip}
```

#### resume.tex

```latex
\documentclass{resume}

\usepackage[left=0.75in,top=0.6in,right=0.75in,bottom=0.6in]{geometry}

\name{John Q. Public}
\address{ 4489 Oxford Lane \\ San Antonio, PA 90024  }
\address{ 555~$\cdot$~356~$\cdot$~7936 \\ jpublic@example.edu }

\def\nameskip{\bigskip}
\def\sectionskip{\medskip}

\begin{document}

  \begin{rSection}{Education}
    {\bf University of California, Berkeley} \hfill {\em June 2004} \\ 
    { B.S. in Computer Science \& Engineering } \\
    { Minor in Linguistics } \smallskip \\
    { Member of Eta Kappa Nu } \\
    { Member of Upsilon Pi Epsilon } \\
    Overall GPA: 5.678
  \end{rSection}
  
  \begin{rSection}{Experience}
  
    \begin{rSubsection}{ACME, Inc}{October 2010 - Present}{Web Developer}{Palo Alto, CA}
    \item Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec a diam lectus.
    \item Donec et mollis dolor. Praesent et diam eget libero Adobe Coldfusion egestas mattis sit amet vitae augue.
    \item Nam tincidunt congue enim, ut porta lorem Microsoft SQL lacinia consectetur.
    \item Donec ut libero sed arcu vehicula ultricies a non tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    \item Pellentesque auctor nisi id magna consequat JavaScript sagittis.
    \item Aliquam at massa ipsum. Quisque bash bibendum purus convallis nulla ultrices ultricies.
    \end{rSubsection}
  
    \begin{rSubsection}{AJAX Hosting}{December 2009 - October 2010}{Lead Developer}{Austin, TX}
    \item Aenean ut gravida lorem. Ut turpis felis, Perl pulvinar a semper sed, adipiscing id dolor.
    \item Curabitur dapibus enim sit amet elit pharetra tincidunt website feugiat nisl imperdiet. Ut convallis AJAX libero in urna ultrices accumsan.
    \item Cum sociis natoque penatibus et magnis dis MySQL parturient montes, nascetur ridiculus mus.
    \item In rutrum accumsan ultricies. Mauris vitae nisi at sem facilisis semper ac in est.
    \item Nullam cursus suscipit nisi, et ultrices justo sodales nec. Fusce venenatis facilisis lectus ac semper.
    \end{rSubsection}

    \begin{rSubsection}{TinySoft}{January 2008 - April 2010}{Web Designer \& Developer}{Gainesville, GA}
    \item Vivamus PostgreSQL fermentum semper porta. Nunc diam velit PHP, adipiscing ut tristique vitae
    \item Maecenas convallis ullamcorper ultricies stylesheets.
    \item Quisque mi metus, unit tests CSS ornare sit amet fermentum et, tincidunt et orci.
    \item Curabitur venenatis pulvinar tellus gravida ornare. Sed et erat faucibus nunc euismod ultricies ut id
    \end{rSubsection}
  
  \end{rSection}
  
  \begin{rSection}{Technical Strengths}
    \begin{tabular}{ @{} >{\bfseries}l @{\hspace{6ex}} l }
      Computer Languages & Prolog, Haskell, AWK, Erlang, Scheme, ML \\
      Protocols \& APIs & XML, JSON, SOAP, REST \\
      Databases & MySQL, PostgreSQL, Microsoft SQL \\
      Tools & SVN, Vim, Emacs
    \end{tabular}
  \end{rSection}

\end{document}
```

