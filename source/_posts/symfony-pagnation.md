---
title: symfony 分页
id: 24
categories:
  - 笔记分享
date: 2012-04-18 14:16:30
tags:
---

<pre lang="php" line="1">
  public function executeShow(sfWebRequest $request)
  {
    $this->category = Doctrine_Core::getTable('Category')->find(array($request->getParameter('id')));
    $this->forward404Unless($this->category);

    $this->pager=new sfDoctrinePager('Content', 1);
    $q=Doctrine::getTable('Content')
    ->createQuery('c')
    ->where('c.category_id=?',array($this->category->getId()));
    $this->pager->setQuery($q);
    if($request->getParameter('page'))
    {
		$this->pager->setPage($request->getParameter('page'));

    }
    $this->pager->init();
  }</pre>

* * *

<pre lang="php" line="1"> 

< ?php foreach($pager->getResults() as $record):?>*   < ?php echo $record->getTitle();?></pre>