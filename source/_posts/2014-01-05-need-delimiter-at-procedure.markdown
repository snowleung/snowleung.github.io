---
layout: post
title: "need delimiter at procedure"
date: 2014-01-05 10:46
comments: true
categories: mysql
---

if use this syntax:

	create procedure your_procedure()
	begin
	 select * from some_table;
	end;
	
you will get syntax error near ''

actually, you may do this:

	delimiter $$
	create procedure your_procedure()
	begin
	 select * from some_table;
	end;
	delimiter ;

fxxk off!!
	