# xcode-breakpoint-issue
Sample app demonstrating issue with Xcode breakpoints in closures

Xcode ignores the "Automatically continue after evaluating actions" and overwrites the configuration of the shared breakpoint on disk:

# Instructions to reproduce issue:

1. Clone repository
2. Notice that the breakpoint in the closure is configured to keep running without stopping execution after evaluating the actions: https://github.com/tspike/xcode-breakpoint-issue/blob/master/BreakpointIssue.xcodeproj/xcshareddata/xcdebugger/Breakpoints_v2.xcbkptlist#L41
3. Run the app
4. Notice that Xcode stops execution (undesired behavior)
5. Further note that Xcode actually overwrites the configuration:

```diff
$ git diff
diff --git a/BreakpointIssue.xcodeproj/xcshareddata/xcdebugger/Breakpoints_v2.xcbkptlist b/BreakpointIssue.xcodeproj/xcshareddata/xcdebugger/Breakpoints_v2.xcbkptlist
index 54532d2..0a72f08 100644
--- a/BreakpointIssue.xcodeproj/xcshareddata/xcdebugger/Breakpoints_v2.xcbkptlist
+++ b/BreakpointIssue.xcodeproj/xcshareddata/xcdebugger/Breakpoints_v2.xcbkptlist
@@ -23,7 +23,7 @@
                   uuid = "9A02F34D-C2B3-4353-A233-5FB6F3947910 - fc12b0f39b69aa25"
                   shouldBeEnabled = "Yes"
                   ignoreCount = "0"
-                  continueAfterRunningActions = "Yes"
+                  continueAfterRunningActions = "No"
                   symbolName = "BreakpointIssue.AppDelegate.application(_: __C.UIApplication, didFinishLaunchingWithOptions: Swift.Optional&lt;Swift.Dictionary&lt;__C.UIApplicationLaunchOptionsKey, Any&gt;&gt;) -&gt; Swift.Bool"
                   moduleName = "BreakpointIssue"
                   usesParentBreakpointCondition = "Yes"
@@ -38,7 +38,7 @@
                   uuid = "9A02F34D-C2B3-4353-A233-5FB6F3947910 - 640319c7285d46c3"
                   shouldBeEnabled = "Yes"
                   ignoreCount = "0"
-                  continueAfterRunningActions = "Yes"
+                  continueAfterRunningActions = "No"
                   symbolName = "closure #1 (Swift.Int) -&gt; Swift.Int in BreakpointIssue.AppDelegate.application(_: __C.UIApplication, didFinishLaunchingWithOptions: Swift.Optional&lt;Swift.Dictionary&lt;__C.UIApplicationLaunchOptionsKey, Any&gt;&gt;) -&gt; Swift.Bool"
                   moduleName = "BreakpointIssue"
                   usesParentBreakpointCondition = "Yes"
```
