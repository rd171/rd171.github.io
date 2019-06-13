---
layout: post
title:  "VC-血压曲线压缩算法Peak-Bottom"
date:   2019-06-13 19:00:00 +0200
categories: VC
---
#### 需求  
血压波形峰值和末值对应高压和低压，当长时间数据压缩时峰值和末值可能因抽样而丢失。
![image](/img/2019-06-13-VC-血压曲线压缩算法Peak-Bottom/0.bmp "image")
#### 方法
采用Peak-Bottom方法进行矢量压缩，即将数据进行分段，并求出段内最大值和最小值，如果当前最大值小于上一次的最小值，则用上次最小值覆盖当前最大值；如果当前最小值大于上次最大值，则用上次最大值覆盖当前最小值。然后将每段最大、最小值相连即可。

#### 代码
```
class CPeakBottomFilter
{
public:
	CPeakBottomFilter()
	{
		m_bLocalFirst = true;
		m_bWholeFirst = true;
	}
	void Clean()
	{
		m_bWholeFirst = true;
	}
	void Calc(double* pData, int nLen)
	{
		if ( nLen <= 0 )
			return;
		for ( int i = 0; i < nLen; i++ )
		{
			if ( m_bLocalFirst )
			{
				m_dLocalMax			= pData[0];
				m_dLocalMin			= pData[0];
				m_bLocalFirst	= false;
			}
			else
			{
				if ( m_dLocalMax < pData[i] )
					m_dLocalMax = pData[i];
				if ( m_dLocalMin > pData[i] )
					m_dLocalMin = pData[i];
			}
			if ( m_bWholeFirst )
			{
				m_dWholeMin			= m_dLocalMin;
				m_dWholeMax			= m_dLocalMax;
				m_bWholeFirst		= false;
			}
		}
	}
	void Get(double& dMax, double& dMin)
	{
		if ( m_dLocalMax < m_dWholeMin )
			m_dLocalMax = m_dWholeMin;
		if ( m_dLocalMin > m_dWholeMax )
			m_dLocalMin = m_dWholeMax;
		dMax = m_dLocalMax;
		dMin = m_dLocalMin;
		m_dWholeMin			= m_dLocalMin;
		m_dWholeMax			= m_dLocalMax;
		m_bLocalFirst		= true;
	}
protected:
	double m_dLocalMax;
	double m_dLocalMin;
	double m_dWholeMax;
	double m_dWholeMin;
	bool   m_bLocalFirst;
	bool   m_bWholeFirst;
};
```
#### 未采用Peak-Bottom效果
![image](/img/2019-06-13-VC-血压曲线压缩算法Peak-Bottom/1.bmp "image")

#### 采用Peak-Bottom效果
![image](/img/2019-06-13-VC-血压曲线压缩算法Peak-Bottom/2.bmp "image")
