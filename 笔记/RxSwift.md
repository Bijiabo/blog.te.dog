# RxSwift 笔记
感觉很有意思
- - - - -

报错：
```
error: use of unresolved identifier 'NopDisposable'
    return NopDisposable.instance
               ^~~~~~~~~~~~~
```
解决：
` return NopDisposable.instance` 替换为 `return Disposables.create()`

- - - - -
