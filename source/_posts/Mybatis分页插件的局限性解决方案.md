---
title: Mybatis分页插件的局限性解决方案
date: 2018-12-14 12:49:12
tags: Java SpringBoot 分页
---

# Java自定义分页工具类

## 1、为什么要写这个工具类：
> **Mybatis 分页插件只能够对mapper的select返回的数据进行分页操作，而要对分页数据进行包装的话，目前只能自定义工具类了，我还没有找到合适的解决办法。**

## 2、代码实现如下：
```java
import java.util.ArrayList;
import java.util.List;

/**
 * @author ZSCDumin
 * @version 1.0
 * @description: 自定义分页工具类：传递参数只需要(要分页的数组,当前页,每页大小)
 * @date 2018/12/13 21:10
 */
public class MyPageHelper<T> {

    private List<T> list;//要分页的数组
    private Integer total; //总个数
    private Integer currentPage; //当前页
    private Integer totalPages; //总页数
    private Integer pageSize; // 每页个数大小
    private Integer previousPage; //前一页
    private Integer nextPage;//后一页

    public Integer getPreviousPage() {
        return previousPage;
    }

    public void setPreviousPage() {
        this.previousPage = currentPage > 0 ? currentPage - 1 : currentPage;
    }

    public Integer getNextPage() {
        return nextPage;
    }

    public void setNextPage() {

        this.nextPage = currentPage < totalPages ? currentPage + 1 : currentPage;
    }

    public List<T> getList() {
        return list;
    }

    public void setList(List<T> list) {
        this.list = list;
    }

    public Integer getTotal() {
        return total;
    }

    public void setTotal() {
        this.total = list.size();
    }

    public Integer getCurrentPage() {
        return currentPage;
    }

    public void setCurrentPage(Integer currentPage) {
        this.currentPage = currentPage;
    }

    public Integer getTotalPages() {
        return totalPages;
    }

    public void setTotalPages() {
        this.totalPages = (int) Math.ceil(1.0 * total / pageSize);
    }

    public Integer getPageSize() {
        return pageSize;
    }

    public void setPageSize(Integer pageSize) {
        this.pageSize = pageSize;
    }

    /**
     * @param list
     * @param currentPage
     * @param pageSize
     */
    public MyPageHelper(List<T> list, Integer currentPage, Integer pageSize) {
        this.list = list;
        this.currentPage = currentPage;
        this.pageSize = pageSize;
        setTotal();
        setTotalPages();
        setNextPage();
        setPreviousPage();
        getResult();
    }

    /**
     * 获取结果
     */
    public void getResult() {
        if (pageSize < total && pageSize > 0) {// 每页小于总数目
            int start = 0, end = 0;
            if (currentPage < totalPages - 1 && currentPage >= 0) {
                start = currentPage * pageSize;
                end = (currentPage + 1) * pageSize - 1;
                setData(start, end);
            } else if (currentPage == totalPages - 1) {
                start = currentPage * pageSize;
                end = total - 1;
                setData(start, end);
            }
        }
    }

    /**
     * 获取数组指定位置的元素
     *
     * @param start 起始位置
     * @param end   截止位置
     * @return
     */
    void setData(int start, int end) {
        if (start >= 0 && end < total) {
            List<T> list1 = new ArrayList<>();
            for (int i = start; i <= end; i++) {
                list1.add(list.get(i));
            }
            this.list.clear();
            setList(list1);
        }
    }
}
```

## 3、使用方式
```java
MyPageHelper<User> myPageHelper = new MyPageHelper<>(list, pageNum, pageSize);
```