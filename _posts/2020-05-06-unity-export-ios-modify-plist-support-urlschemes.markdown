---
layout:  	post
title:  "Unity修改plist"
date:   2020-05-06
author:  "newstrong"
header-img: ""
tags:
    -技术
    -Android
    -Unity
    -iOS
    -交互
---



# Unity修改plist

> Unity导出iOS工程通过PostProcessBuildAttribute需改plist文件，增加UrlScheme支持和Facebook appid

~~~
#if (UNITY_5 && UNITY_IOS) || UNITY_IPHONE

using System.IO;
using UnityEditor;
using UnityEditor.Callbacks;
using UnityEditor.iOS.Xcode;
using UnityEngine;

public static class Test
{
    [PostProcessBuildAttribute(1)]
    public static void OnPostProcessBuild(BuildTarget buildTarget, string path)
    {

        string plistPath = Path.Combine(path, "Info.plist");
        PlistDocument plist = new PlistDocument();
        plist.ReadFromFile(plistPath);
        //删除UIApplicationExitsOnSuspend
        plist.root.values.Remove("UIApplicationExitsOnSuspend");

        // 追加URL schemes
        var urlTypeArray = plist.root.CreateArray("CFBundleURLTypes");
        var urlTypeDict = urlTypeArray.AddDict();
        urlTypeDict.SetString("CFBundleTypeRole", "Editor");
        urlTypeDict.SetString("CFBundleURLName", "penetratedata");
        var urlScheme = urlTypeDict.CreateArray("CFBundleURLSchemes");
        urlScheme.AddString("xx00");
        urlScheme.AddString("fb12345678");

        plist.root.SetString("FacebookAppID","519348645266138");
        plist.root.SetString("FacebookDisplayName","xx oo");
        var queriesArrays=plist.root.CreateArray("LSApplicationQueriesSchemes");
        queriesArrays.AddString("fbapi");
        queriesArrays.AddString("fb-messenger-share-api");
        queriesArrays.AddString("fbauth2");
        queriesArrays.AddString("fbshareextension");

        plist.root.SetString("NSCalendarsUsageDescription","This app need to access your calendar events");

        File.WriteAllText(plistPath, plist.WriteToString());

    }
}

#endif
~~~




