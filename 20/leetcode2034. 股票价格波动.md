### 解题思路
- 用一个多重集合（可重集合）来记录当前股票的价格
- 每次更新时，如果时间存在对应的股票价格，就删除原先的价格
- 更新多重集（股票价格）
- 维护最新的股票的价格以及时间戳
- `multiset` 数据结构自动排序，最左/最右，即为：最小/最大

### 代码

```cpp
class StockPrice {
private:
    multiset<int>s;
    unordered_map<int,int>time2price;
    int lastTime=0,lastPrice=0;    
public:
    StockPrice(){}    
    void update(int timestamp, int price){        
        //维护记录的股票价格的集合
        if(time2price.count(timestamp))
            s.erase(s.find(time2price[timestamp]));
        time2price[timestamp]=price;
        s.insert(price);
        //维护最新股票价格和时间
        if(timestamp>=lastTime)
            lastTime=timestamp,lastPrice=price;        
    }    
    int current(){return lastPrice;}
    int maximum(){return*s.rbegin();}
    int minimum(){return*s.begin();}
};

```
