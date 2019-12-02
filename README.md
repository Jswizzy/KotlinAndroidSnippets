# KotlinAndroidSnippets
Android code snippets


** Intents

```Kotlin
  fun Context.launchIntent(intent: Intent): Result<Unit> {
    return if (intent.resolveActivity(packageManager) != null) {
        startActivity(intent)
        Result.success(Unit)
    } else {
        Result.failure(ActivityNotFoundException())
    }
}

fun Context.isPackageExist(target: String): Boolean {
    return this.packageManager.getInstalledApplications(0).find { info ->
        info.packageName == target
    } != null
}
```
