# NextJS

NextJS ist ein Fullstack React Framework, d. h. es besteht sowohl aus Server- als auch aus Clientteilen. Der große Vorteil eines solchen Fullstack Frameworks ist, dass man die Applikation "in einem Guß" entwickeln kann. Derzeit ist die Version 15 von NextJS aktuell.

## Komponenten

Standardmäßig sind Komponenten in NextJS Serverkomponenten, d. h. sie werden am Server gerendert. Außerdem gibt es noch Clientkomponenten, die am Client gerendert werden. Serverkomponenten kann man sich wie die API oder das Backend seiner Applikation vorstellen. Dort kann man beispielsweise direkt auf die Datenbank zugreifen, aber man kann andererseits keine "Interaktivität" ermöglichen. Auf der anderen Seite sind Clientkomponenten dafür gedacht, die Interaktivität mit dem Benutzer herzustellen. Sie laufen am Client (im Browser).

Um eine Komponente zu einer Client Komponente zu machen, muss man ganz am Anfang des Files, wo die Komponente definiert ist `'use client';` verwenden. Mit `'use server';` erstellt man eine Serverkomponente (diese Angabe ist aber nicht explizit notwendig, weil eben Server Komponenten der Standard sind).
