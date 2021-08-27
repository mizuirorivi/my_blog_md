

# Nest-js カスタムデコレータの作成

###### tags: `nest-js`

```typescript
import { createParamDecorator, ExecutionContext,BadRequestException } from '@nestjs/common'
import * as admin from 'firebase-admin'

export const CustomHeaders =  createParamDecorator(
  (data: string, ctx: ExecutionContext) => {
    const req = ctx.switchToHttp().getRequest()
    const value = req.headers[data].split('Bearer ')[1]
    
    return admin.auth().verifySessionCookie(value, true).then((decodedClaims) => {
        return decodedClaims.user_id
    }).catch(err => {
        console.log("err:",err)
        throw new BadRequestException('Error:Validation failed. Is the authorization appropriate?');
    })
  }
)

```



```typescript
@Post()
  async CreatePdf(@CustomHeaders('authorization') uid) {
    const result = await this.pdfService.CreatePdf(uid)
    return result
  }
```



## 解説

firebaseのセッションを受け取って(ヘッダーに添付),userIdを返すPipeを作ろうとしたが、既存のデコレータ(@Header())はPipeに互換性がなかったため、セッションを受け取ってuseridを返すデコレータを作った。

## 参照

https://docs.nestjs.com/custom-decorators

