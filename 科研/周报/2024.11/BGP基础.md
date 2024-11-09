# BGP基础

## HoldTime

BGP邻居关系中允许的最大无消息间隔时间，超出这个时间就会终止BGP会话

默认180s

### Keepalive Timer

通常设置为1/3 Hold Timer

### Connect Retry Timer

连接失败后的重试间隔

### 工作流程

1. BGP会话建立时，双方交换OPEN消息，协商Hold Time
2. 采用双方宣告的较小值作为最终Hold Time
3. 会话建立后，双方定期发送Keepalive消息
4. 每收到一个BGP消息（包括Keepalive），Hold Timer重置
5. 如果Hold Timer超时，BGP会话立即断开

### Bird2配置

```shell
birdc show protocols all bgp1 # 检查当前Hold Time设置
birdc show protocols bgp1 # 查看BGP会话状态和计时器
```

```bash
# 调整HoldTime
protocol bgp {
    # 更激进的设置（不建议在生产环境使用）
    hold time 90;        # 更短的hold time
    keepalive time 30;   # 更频繁的keepalive
}
```

