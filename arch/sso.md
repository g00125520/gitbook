# sso

302到9003进行登陆，登陆验证成功之后在cookie中生成gov-sid，然后通过gov-sid获取code，通过code获取token，通过token获取对应用户信息。当点击其他系统链接时，其他系统首先302到9003，由于cookie中存在gov-sid，所以系统可以直接通过gov-sid获取code，通过code获取token，通过token获取用户信息从而登陆成功。


