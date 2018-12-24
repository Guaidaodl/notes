之前对 clipChildren 的理解是有误.

从描述来看, clipChildren 允许 children 绘制在 parent 之外的部分. 很容易被误解成 children 在 parent 之外的部分也是可见的.
实际情况是允许绘制, 但是并不可见.

但是如果对 View 进行变换, 可能会让原本不可见的部分变成可见. 如果这时候 clipChildren 属性的作用就能体现了. 如果 clipChildren 为
true View 就会截断.
