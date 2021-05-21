---
title: Unity3D SimpleAnimation
date: 2021-05-20 22:39:38
tags: Unity
---

Unity 播放动画的三种方式

参考文献：https://blog.csdn.net/u010019717/article/details/86633601

1.Animation(Legacy) 

2.Mecanim(Animator,AnimatorController,Avatar)

<!-- more -->

3. ##### Playable,Timeline(PlayableDirector,PlayableAsset,官方示例 SimpleAnimation)

   playable 创建动画流程:  

   1.Create Graph

   2.Create Playable

   3.Create PlayableOutput. (AnimationPlayableOutput, AudioPlayableOutput,ScriptPlayableOutput)

   4.playableoutput SetSourcePlayable(playable)

   5.graph.Play()

   AnimationPlayableUtilities 