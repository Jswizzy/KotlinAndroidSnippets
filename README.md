# KotlinAndroidSnippets
Android code snippets

* [Interacting with Apps](#Interacting-with-Apps)

## Interacting with Apps

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

fun Context.startActivityWithPackage(intent: Intent, packageName: String) = runCatching {
    if (isPackageExist(packageName)) {
        intent.`package` = packageName
        startActivity(intent)
    } else {
        try {
            startActivity(
                Intent(
                    Intent.ACTION_VIEW,
                    Uri.parse("market://details?id=$packageName")
                )
            )
        } catch (e: ActivityNotFoundException) {
            startActivity(
                Intent(
                    Intent.ACTION_VIEW,
                    Uri.parse("https://play.google.com/store/apps/details?id=$packageName")
                )
            )
        }
    }
}
```
