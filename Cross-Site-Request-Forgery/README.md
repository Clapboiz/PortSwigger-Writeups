## Challenge 1: CSRF vulnerability with no defenses
## Challenge 2: CSRF where token validation depends on request method
## Challenge 3: CSRF where token validation depends on token being present
## Challenge 4: CSRF where token is not tied to user session
## Challenge 5: CSRF where token is tied to non-session cookie
## Challenge 6: CSRF where token is duplicated in cookie
## Challenge 7: SameSite Lax bypass via method override
## Challenge 8: SameSite Strict bypass via client-side redirect
## Challenge 9: SameSite Strict bypass via sibling domain
## Challenge 10: SameSite Lax bypass via cookie refresh
## Challenge 11: CSRF where Referer validation depends on header being present
## Challenge 12: CSRF with broken Referer validation
**1 Vài lưu ý về same site là:**

Nếu không có SameSite hoặc nếu SameSite=None, cookie sẽ được gửi kèm trong mọi loại yêu cầu, bất kể đó là GET hay POST, và bất kể yêu cầu có đến từ cùng site hay từ một site khác. Điều này có nghĩa là cookie sẽ luôn được gửi đi nếu bạn truy cập vào trang web có cookie từ bất kỳ nguồn nào.

Tuy nhiên, khi bạn áp dụng SameSite:

+ Với SameSite=Lax, cookie chỉ được gửi kèm trong các yêu cầu GET điều hướng trực tiếp từ cùng một site hoặc từ một trang khác (như khi nhấp vào liên kết dẫn đến trang đó), nhưng sẽ không gửi cookie kèm với các yêu cầu POST hoặc các yêu cầu không phải điều hướng từ trang khác.

+ Với SameSite=Strict, cookie chỉ được gửi kèm trong các yêu cầu đến từ cùng site và sẽ không được gửi kèm trong bất kỳ yêu cầu nào từ trang ngoài, kể cả GET điều hướng.
