<https://leetcode.com/problems/validate-ip-address/>

Check separately for IPv4 and IPv6. A trick here is using `str(int(part)) != part` to check if there's leading zero in a number.

```python
class Solution:
    def validIPAddress(self, IP: str) -> str:
        
        def ipv4(ip):
            parts = ip.split('.')
            if len(parts) != 4:
                return False
            for part in parts:
                try:
                    if int(part) > 255 or int(part) < 0 or str(int(part)) != part:
                        return False
                except:
                    return False
            return True
        
        def ipv6(ip):
            parts = ip.split(':')
            if len(parts) != 8:
                return False
            for part in parts:
                if len(part) == 0 or len(part) > 4:
                    return False
                for char in part:
                    if not ('0' <= char <= '9' or 'a' <= char <= 'f' or 'A' <= char <= 'F'):
                        return False
            return True
        
        if ipv4(IP):
            return 'IPv4'
        elif ipv6(IP):
            return 'IPv6'
        else:
            return 'Neither'
```

