```kotlin
fun View.showWithCondition(isShown: Boolean) {
    visibility = if (isShown) View.VISIBLE else View.GONE
}

fun View.show() {
    visibility = View.VISIBLE
}

fun View.hide() {
    visibility = View.GONE
}

fun View.invisible() {
    visibility = View.INVISIBLE
}

fun addItemClick(vararg view: View, listener: SingleViewClickListener) {
    view.forEach { v ->
        registerSingleClick(v) {
            listener.onSingleViewClick(it)
        }
    }
}

fun registerSingleClick(view: View, callback: (View) -> Unit) {
    var lastClickEvent = 0L
    val debouncedTime = 100L
    val listener = View.OnClickListener {
        if (SystemClock.elapsedRealtime() < lastClickEvent + debouncedTime) return@OnClickListener
        callback(it)
        lastClickEvent = SystemClock.elapsedRealtime()
    }
    view.setOnClickListener(listener)
}


inline fun SearchView.onQueryTextChanged(crossinline listener: (String) -> Unit) {
    this.setOnQueryTextListener(object : SearchView.OnQueryTextListener {
        override fun onQueryTextSubmit(query: String?) = true

        override fun onQueryTextChange(newText: String?): Boolean {
            listener(newText.orEmpty())
            return true
        }

    })
}

fun Activity.showToast(content: String) {
    Toast.makeText(this, content, Toast.LENGTH_SHORT).show()
}
```