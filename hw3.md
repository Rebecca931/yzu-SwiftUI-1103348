<h1>hw3</h1>
<table>
  <tr>
    <td>
      
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        ZStack{
            VStack {
                Rectangle()
                    .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                    .frame(width: 2500, height: 20)
                    .position(x: 0, y: 0)
                HStack{
                    Rectangle()
                        .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                        .frame(width: 20, height: 2500)
                        .position(x: 0, y: 0)
                    //我把四本書用position的方式把他們靠在一起
                    Image("book1")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                        .position(x: 10, y: 0)
                    Image("book2")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                        .position(x: -15, y: 2)
                    Image("book3")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                        .position(x: -40, y: 4)
                    Image("book4")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center) 
                        .position(x: -65, y: 6)
                    Image("fish")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 150, height: 150, alignment: .top)
                        .position(x: 0, y: 30)
                    Rectangle()
                        .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                        .frame(width: 10, height: 2500)
                        .position(x: 43, y: 0)
                }
                Rectangle()
                    .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                    .frame(width: 2500, height: 10)
                HStack{
                    Image("ink")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                    Image("ribbon")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                    Image("clock")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                    Image("pencil")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 90, height: 90, alignment: .center)
                }
                Rectangle()
                    .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                    .frame(width: 2500, height: 10)
                HStack{
                    VStack{
                        HStack{//使用多個HStack和VStzck把他們放進去
                            Rectangle()
                                .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                                .frame(width: 10, height: 20)
                            Rectangle()
                                .fill(Color(red: 71/255, green: 34/255, blue: 0/255))  
                                .frame(width: 2, height: 20)
                            Image("paper")
                                .resizable()
                                .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                                .frame(width: 70, height: 70, alignment: .center)
                            
                            Image("plant")
                                .resizable()
                                .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                                .frame(width: 80, height: 80, alignment: .center)
                        }
                        Rectangle()
                            .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                            .frame(width: 360, height: 10)
                            .position(x: 0, y: 16)
                        HStack{
                            Rectangle()
                                .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                                .frame(width: 10, height: 20)
                            Rectangle()
                                .fill(Color(red: 71/255, green: 34/255, blue: 0/255))  
                                .frame(width: 2, height: 20)
                            Image("box")
                                .resizable()
                                .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                                .frame(width: 160, height: 160, alignment: .bottom)
                        }
                        
                    }
                    Rectangle()
                        .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                        .frame(width: 10, height: 290)
                        .position(x: 20, y:83)
                    Image("sew")
                        .resizable()
                        .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                        .frame(width: 130, height: 130, alignment: .bottom)
                        .position(x: 0, y: 150)
                }
                Rectangle()
                    .fill(Color(red: 138/255, green: 90/255, blue: 28/255))  
                    .frame(width: 2500, height: 10)
            }
        }
        .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
        .background(Color(red: 71/255, green: 34/255, blue: 0/255))
    }
}


```

<img width = "400"  src="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/IMG_0324.jpeg">
    </td>
  </tr>
</table>
