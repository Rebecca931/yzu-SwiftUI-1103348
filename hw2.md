<h1>hw2</h1>
<table>
  <tr>
      <td>
```swift
//在you點選自己要出的拳,同時opponent會隨機出拳,opponent出的拳會變大
//上面比數會更新,如果平手就都沒有分數,按RESTART分數會歸零

import SwiftUI

struct ContentView: View {
    @State var count:Int = 3 //opponent的隨機出拳，先預設3，所有大小相同
    @State var you:Int = 0 //用來存取使用者按了什麼
    @State var Oscore:Int = 0 //opponent score
    @State var Yscore:Int = 0 //you score
    
    var body: some View {
        VStack{//用VStack一個一個放進去
            Text("Y : O") //左邊是you, 右邊是opponent
                .padding(.all,10)
                .frame(width: 200, height: 30, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                .foregroundColor(Color(red: 160/255, green: 64/255, blue: 0/255))
                .font(.system(size: 50, design: .serif))
            Text(String(Yscore)+" : "+String(Oscore))//表示比數
                .padding(.all,10)
                .frame(width: 420, height: 80, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                .foregroundColor(.white)
                .font(.system(size: 50, design: .serif))
            Text("OPPONENT")
                .padding(.all,10)
                .frame(width: 250, height: 50, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                .font(.system(size: 30, design: .serif))
                .background(Color(red: 215/255, green: 189/255, blue: 226/255))
                .foregroundColor(Color(red: 160/255, green: 64/255, blue: 0/255))
            HStack{//用HStack表示三種拳
                if(count == 3){//預設三種都一樣大
                    Image("2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 130, height: 130, alignment: .top)
                    Image("0")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 130, height: 130, alignment: .top)
                    Image("5")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 130, height: 130, alignment: .top)
                }
                if(count == 0){//表示出石頭
                    Image("2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                    Image("0")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 150, height: 150, alignment: .top)
                    Image("5")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                }
                if(count == 1){//表示出剪刀
                    Image("2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 150, height: 150, alignment: .top)
                    Image("0")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                    Image("5")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                }
                if(count == 2){//表示出布
                    Image("2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                    Image("0")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 105, height: 105, alignment: .top)
                    Image("5")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 150, height: 150, alignment: .top)
                }
                
            }
            
            Text("YOU")
                .padding(.all,10)
                .frame(width: 250, height: 50, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                .font(.system(size: 30, design: .serif))
                .background(Color(red: 245/255, green: 183/255, blue: 177/255))
                .foregroundColor(Color(red: 160/255, green: 64/255, blue: 0/255))
            HStack{
                Button(action: {
                    let randomInt = Int.random(in:0...2)
                    self.count = randomInt
                    self.you = 0
                    if(count==0){
                        self.Oscore += 1
                    }
                    if(count==2){
                        self.Yscore += 1
                    } 
                }, label: {
                    Image("2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 115, height: 115, alignment: .bottom)
                })
                Button(action: {
                    let randomInt = Int.random(in:0...2)
                    self.count = randomInt
                    self.you = 1
                    if(count==2){
                        self.Oscore += 1
                    }
                    if(count==1){
                        self.Yscore += 1
                    } 
                }, label: {
                    Image("0")
                        .resizable()
                        .aspectRatio(contentMode: .fill)
                        .frame(width: 115, height: 115, alignment: .bottom)
                })
                Button(action: {
                    let randomInt = Int.random(in:0...2)
                    self.count = randomInt
                    self.you = 2
                    if(count==1){
                        self.Oscore += 1
                    }
                    if(count==0){
                        self.Yscore += 1
                    } 
                }, label: {
                    Image("5")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 115, height: 115, alignment: .bottom)
                })
                
            }
            Button(action: {
                self.count = 3
                self.you = 0
                self.Yscore = 0
                self.Oscore = 0
            }, label: {
                Text("RESTART")
                    .padding(.all,10)
                    .frame(width: 230, height: 110, alignment: /*@START_MENU_TOKEN@*/.center/*@END_MENU_TOKEN@*/)
                    .font(.system(size: 50))
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 174/255, green: 214/255, blue: 241/255), Color(red: 248/255, green: 196/255, blue: 113/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .border(LinearGradient(gradient: Gradient(colors: [Color(red: 174/255, green: 214/255, blue: 241/255), Color(red: 248/255, green: 196/255, blue: 113/255)]), startPoint: .leading, endPoint: .trailing), width: 1)
                    .cornerRadius(20)
            })
            
        }
        
        .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
        .background(Color(red: 215/255, green: 240/255, blue: 187/255))
    }
}


```
    <video width = "400" src = "https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-    1103348/main/hw2_video.mp4">
    </video>

    </td>
    
  </tr>
</table>
