# B-H FDR讨论		

​		关于B-H FDR，就跟师兄发的博客里(https://brainder.org/2011/09/05/fdr-corrected-fdr-adjusted-p-values/)所述，十分详尽，具体实现有两种方案：

* 任意输入N个p value，以及q(即FDR阈值，0.05)，输出被拒绝或者被接受的Null Hypothesis。

  大致过程为：

  1. 对p value从小到大排序，排序后则有$p_{(1)} \leq p_{(2)} \leq \ldots \leq p_{(N)}$

  2. 根据准则(1)
     $$
     p_{(i)} \leq \frac{i}{N} \frac{q}{c(N)}
     $$
     其中$c(N)=1$或者 $c(N)=\sum_{i=1}^{N} 1 / i$  可供选择

     需要找到最大的第$k$个满足准则(1)的$i$，则  $p_{(1)},p_{(2)}...p_{(k)}$  均被拒绝，$p_{(k+1)}...p_{(n)}$均不被拒绝
     
      并不是满足准则(1)都通过(被拒绝)，例如：
     
      排序后的7个p value为：
     
      		0.0050    0.0100    0.0200    **0.0300**    0.0300    0.0400    0.0500
     
      计算准则(1)不等式右边 $\frac{i}{N} \frac{q}{c(N)}$ 的值分别为：
      		0.0071    0.0143    0.0214    **0.0286**    0.0357    0.0429    0.0500	
      正确的结果应该是所有7个p value都通过，而不是通过6个。 

  3. 将排序后的p value的通过与否情况，还原为原始未排序的p value 的输出。

  

​		以上过程已有代码可以说只实现了一部分，并且语义有一定的问题，输出的分别是两种$c(N)$准则下通过FDR的某个初始的p value。原始代码如下：

  ```matlab
  function [pID,pN] = IPN_FDR(p,q)
      p=sort(p(:));
      V = length(p);
      I = (1:V)';
      cVID=  1;
      cVN = sum(1./(1:V));
  
      pID  = p(max(find(p<=I/V*q/cVID)));
      pN = p(max(find(p<=I/V*q/cVN)));
  end
  ```



* 第二种实现方案则为：输入任意N个p value，输出对应的**"adjusted p"**，再进一步根据adjusted p判断小于某个阈值的通过BHFDR.
  大致过程为：

  1. 对p value从小到大排序，排序后则有$p_{(1)} \leq p_{(2)} \leq \ldots \leq p_{(N)}$

  2. FDR correction：
     计算
     $$
     q_{(i)}=\frac{p_{(i)} N}{i} c(N)
     $$
     此处的$q$的含义不同于第一种方案的$q$。

  3. FDR adjustment：
     $q^*(i)$ is the smallest $q(k)$，$k>=i$;

  4. 排序后的N个p_adjusted映射回原始的顺序。

  

  实现代码：

  ```matlab
  function p_adjusted = my_FDR(pvalue)
      % sort
      pvalue = pvalue(:);
      n = length(pvalue);
      i = (1:n)';
      [p_sorted,idx] = sort(pvalue,'ascend');
      
      % Correct
      q = p_sorted * n ./ i ;
      
      % Adjustment
      for j = (length(q)-1):-1:1
          if q(j)>q(j+1)
              q(j) = q(j+1);
          end
      end
      
      % convert to original index
      [~,oriIdx] = sort(idx,'ascend');
      p_adjusted = q(oriIdx);
  end
  ```

  使用方法：`myFDR(pvalue)`；
  返回结果和使用Matlab的库函数`mafdr(pvalues,'BHFDR',true)`完全一致。

  得到``p_adjusted`之后就可以卡不同的阈值判断FDR校正的结果。

