---
layout: post
title: VBA Macro to send email with attachment as per the recepient list in excel
  sheet
date: 2012-06-26 13:58:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5585184604437936652'
---
<div dir="ltr" style="text-align:left;">1) Open New Excel sheet and mention user Name , Email ID &amp; Score/Report in sequential cells in second row as first will cover their titles <br />2) copy and paste below code into the relevant macro window , choose any attachment by editing code accordingly and run it to see the magic  </p>
<p>Sub SendEmail()<br /> 'Works in 2000-2007<br />    Dim EmailDist As String<br />    Dim AcWB As <span class="IL_AD" id="IL_AD7">Workbook<span class="IL_AD_ICON"></span></span><br />    Dim OutApp As Object<br />    Dim OutMail As Object<br />    Dim str As String<br />    Dim r As Integer, x As Double<br />    Dim xint As Long<br />    <br />        For r = 2 To 4<br />    Set OutApp = CreateObject("Outlook.<span class="IL_AD" id="IL_AD3">Application<span class="IL_AD_ICON"></span></span>")<br />    OutApp.Session.Logon<br />    Set OutMail = OutApp.CreateItem(0)</p>
<p>    'Date the Email is being sent<br />    'strDate = Format(Date, "dddd, mmm d yyyy")<br />  <br />    'Distribution list</p>
<p>    strAddress = Cells(r, 2)<br />  <br />    strSubject = "Your Online Exam Score"<br />    strBody = ""<br />          <br />     On Error GoTo JUSTEND<br />     With OutMail<br />        .To = strAddress<br />        .Subject = strSubject<br />        .HTMLBody = "Please Check the attachment"<br />         'Attach file here with complete path to file plus filename and file extension.<br />         .Attachments.Add "C:\abc.txt"<br />         .Send<br />            End With<br />JUSTEND:<br />          <br />    Set OutMail = Nothing 'Remove <span class="IL_AD" id="IL_AD6">from memory<span class="IL_AD_ICON"></span></span><br />    Set OutApp = Nothing 'Remove from memory<br />     Next r<br />  <br />End Sub</div>
