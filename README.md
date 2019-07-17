The files in this repo were generated with:

```clojure
(let [data (repeat 10000 {:example.ns/broken? true, :example.ns/problem :overflow})]
  (binding [*print-namespace-maps* true
            *print-length* nil]
    (spit "resources/compact-map.edn" (pr-str data))))
```

Opening this repo in Cursive yields a stack overflow exception during indexing the version with namespaced maps:

```
2019-07-16 16:22:56,569 [  20073]  ERROR - napi.project.CacheUpdateRunner - Error while indexing /path/to/compact-map.edn
To reindex this file IDEA has to be restarted 
java.lang.StackOverflowError
	at com.intellij.openapi.progress.ProgressManager.checkCanceled(ProgressManager.java:204)
	at com.intellij.openapi.progress.ProgressIndicatorProvider.checkCanceled(ProgressIndicatorProvider.java:46)
	at com.intellij.psi.impl.source.tree.CompositeElement.getPsi(CompositeElement.java:721)
	at com.intellij.psi.impl.source.SourceTreeToPsiMap.treeElementToPsi(SourceTreeToPsiMap.java:30)
	at com.intellij.psi.impl.source.tree.SharedImplUtil.getNextSibling(SharedImplUtil.java:60)
	at com.intellij.psi.impl.source.tree.LeafPsiElement.getNextSibling(LeafPsiElement.java:76)
	at cursive.psi$next_siblings$fn__452.invoke(psi.clj:345)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$filter$fn__4580.invoke(core.clj:2679)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:56)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$concat$fn__4215.invoke(core.clj:691)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$concat$cat__4217$fn__4218.invoke(core.clj:700)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$concat$cat__4217$fn__4218.invoke(core.clj:700)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$concat$cat__4217$fn__4218.invoke(core.clj:700)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	at clojure.core$concat$cat__4217$fn__4218.invoke(core.clj:700)
	at clojure.lang.LazySeq.sval(LazySeq.java:40)
	at clojure.lang.LazySeq.seq(LazySeq.java:49)
	at clojure.lang.RT.seq(RT.java:507)
	at clojure.core$seq__4128.invoke(core.clj:137)
	... (200 more stack iterations omitted) ...
2019-07-16 16:22:56,578 [  20082]  ERROR - napi.project.CacheUpdateRunner - IntelliJ IDEA 2018.3.6  Build #IU-183.6156.11 
2019-07-16 16:22:56,578 [  20082]  ERROR - napi.project.CacheUpdateRunner - JDK: 1.8.0_152-release; VM: OpenJDK 64-Bit Server VM; Vendor: JetBrains s.r.o 
2019-07-16 16:22:56,578 [  20082]  ERROR - napi.project.CacheUpdateRunner - OS: Mac OS X 
2019-07-16 16:22:56,579 [  20083]  ERROR - napi.project.CacheUpdateRunner - Plugin to blame: Cursive version: 1.8.2-eap4-2018.3 
```

Tested on:
* IntelliJ `2018.3.6` with Cursive `1.8.2-eap4-2018.3`
