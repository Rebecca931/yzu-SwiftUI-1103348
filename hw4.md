<h1>hw4</h1>
<table>
    <tr>
    <td>
      
```swift
import SwiftUI

struct ContentView: View {
    //將使用者的名字新增到頁面上
    @AppStorage("UserName") var UserName:String = ""
    
    var body: some View {
        VStack {
            Text("🤩推薦的片單🤩")
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
            HStack{
                Text("使用者: ")
                    .font(.system(size: 18))
                Text(UserName.isEmpty ?"" : UserName)
                    .font(.system(size: 18))    
            }
            TabView{
                Group{
                    WelcomeView()
                        .tabItem { 
                            Image(systemName: "rosette")
                            Text("Welcome")
                        }
                    DisneyListView()
                        .tabItem { 
                            Image(systemName: "list.bullet")
                            Text("Disney Movies")
                        }
                    AnimeListView()
                        .tabItem { 
                            Image(systemName: "film.stack.fill")
                            Text("Anime")
                        }
                    TaiwanListView()
                        .tabItem { 
                            Image(systemName: "play.square.stack")
                            Text("Taiwanese films")
                        }
                    CardView()
                        .tabItem { 
                            Image(systemName: "book")
                            Text("今天看什麼!!!")
                        }
                    progressView()
                        .tabItem { 
                            Image(systemName: "percent")   
                            Text("完成進度")
                        }
                    SettingView()
                        .tabItem { 
                            Image(systemName: "wrench.adjustable")
                            Text("settings")
                        }
                }
            }
        }.padding(.top, 20)
            .tint(Color(red: 160/255, green: 64/255, blue: 119/255)) //被點擊的TabItem顏色
            .onAppear(perform: {
                UITabBar.appearance().backgroundColor = UIColor(Color(red: 231/255, green: 209/255, blue: 224/255)) //TabView背景顏色
                
                UITabBar.appearance().unselectedItemTintColor = UIColor(Color(red: 52/255, green: 167/255, blue: 199/255))//沒被點擊的TabItem顏色
            })
            .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
            .background(Color(red: 231/255, green: 209/255, blue: 224/255))//APP背景顏色
    }
}
```
<img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/welcome.gif">
   </td>
    </tr>

    <tr>
    <td>
      
```swift
import SwiftUI
//首頁的畫面

struct WelcomeView: View {
    var body: some View {
        VStack {
            Image("film")
                .resizable()
                .aspectRatio(contentMode: .fill)
               .frame(width: 340, height: 340, alignment: .center)
            Text("推薦給你💁🏻‍♀️\n看都看不完的好片")
                .font(.system(size: 40, weight: .bold, design: .rounded))
                .lineSpacing(10)
                .foregroundStyle(Color(red: 255/255, green: 145/255, blue: 25/255))
                .fontWeight(.heavy)
                .lineSpacing(10)
                .frame(width: 350, height: 150, alignment: .center)
                .background(Color(red: 215/255, green: 240/255, blue: 187/255))
                .cornerRadius(30.0)
                .opacity(0.8)
                .multilineTextAlignment(.center)
            
        }.padding(.top, 20)
    }
}

```

<img width = "400"  src="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/IMG_0489.jpeg">

   </td>
   </tr>

   
   <tr>
   <td>

```swift
import SwiftUI
//用List來呈現disney的片單

struct Disney: Identifiable{
    var id = UUID()
    var image:String
    var DisneyNameUS:String //故事簡介
    var DisneyNameTW:String //中文片名
    var DisneyHours:String //上映時間
    var predict:String //預告片網址
}

var disney = [ //片單陣列
    Disney(image: "coco", DisneyNameUS: "故事講述一個名為米高·李維拉的11歲男孩意外穿越到亡靈的世界，他需要尋求自己的已故音樂家曾外祖父的幫助，把他送返現實世界", DisneyNameTW: "可可夜總會", DisneyHours: "2017/11/22", predict: "https://youtu.be/KtbCQDXiBdE?si=0RSIHfyC4u3SOBnU"),
    Disney(image: "brain", DisneyNameUS: "萊莉因為父親工作的因素舉家搬遷至舊金山，要準備適應新環境，但就在此時，萊莉腦中控制歡樂與憂傷的兩位腦內大臣- 樂樂與憂憂迷失在茫茫腦海中。\n大腦總部只剩下掌管憤怒、害怕與厭惡的三位幹部負責，導致本來樂觀的萊莉變成憤世嫉俗少女。樂樂與憂憂必須要盡快在複雜的腦中世界回到大腦總部，讓萊莉重拾原本快樂正常的情緒…。", DisneyNameTW: "腦筋急轉彎", DisneyHours: "2015/05/18", predict: "https://www.youtube.com/watch?v=1T_LbO3DqCM"),
    Disney(image: "brave", DisneyNameUS: "蘇格蘭高地擅使弓箭的公主梅莉達因為與母親艾琳諾皇后對未來的期盼產生分歧，發生爭執的過程意外導致母親被魔咒變成一頭熊，這使得梅莉達必須和艾琳諾皇后展開冒險，找出解除魔咒的方法。", DisneyNameTW: "勇敢傳說", DisneyHours: "2012/06/22", predict: "https://www.youtube.com/watch?v=UBiuNTx8wNk"),
    Disney(image: "frozen", DisneyNameUS: "擁有皇家血統的安娜被姊妹艾莎所詛咒，為解除詛咒，她與冒險的山民、馴鹿及雪人，一起踏上北上的路程...。", DisneyNameTW: "冰雪奇緣1", DisneyHours: "2013/12/27", predict: "https://www.youtube.com/watch?v=dQoR5WyfqQs"),
    Disney(image: "animal", DisneyNameUS: "在動物方城市裡，茶蒂哈普斯警官作為警隊里的第一任免子警官，下定決心證明自己。這就是為什麼她會抓住破案的機會，即使這意味著要和語速很快的狐狸騙子胡尼克合作來解開這個謎國。", DisneyNameTW: "動物方城市", DisneyHours: "2016/03/04", predict: "https://www.youtube.com/watch?v=v5ylDdPZm9A"),
    Disney(image: "sea", DisneyNameUS: "取材於太平洋島嶼玻里尼西亞文化流傳許久的毛伊半神人故事，主角莫娜的族人在島嶼上安居樂業，直到有一天，漁獲數量漸漸短少，而且農作物也減少產值，樹木慢慢枯死…莫娜的阿嬤告訴她一個神祕的傳說──大地之母本來擁有一顆海洋之心，但是卻被一位半神人毛伊取走，因此釋放了黑暗力量，生態的平衡受到了破壞，莫娜的使命則是找到半神人毛伊，請他歸還海洋之心，讓一切恢復原狀…。", DisneyNameTW: "海洋奇緣", DisneyHours: "2016/10/23", predict: "https://www.youtube.com/watch?v=0PjI4AyCEkw"),
    
]

struct DisneyListView: View {
    @State var showDetialView = false
    @State var selectedDisney: Disney?
    var body: some View {
        NavigationView{
            List(disney){DisneyItem in
                BasicImageRow(thisDisney : DisneyItem)
                    .onTapGesture {
                        self.showDetialView = true
                        self.selectedDisney = DisneyItem
                    }
            }
            .sheet(item: self.$selectedDisney, content: {DisneyItem in
                DisneyDetialView(thisDisney: DisneyItem)
            })
            .navigationTitle("迪士尼電影")
        }
    }
}

struct BasicImageRow: View {
    var thisDisney: Disney
    var body: some View {
        HStack{
            Image(thisDisney.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thisDisney.DisneyNameTW)
        }
    }
}

struct DisneyDetialView: View {
    @Environment(\.presentationMode)
    var presentationMode
    var thisDisney: Disney
    var body: some View {
        ScrollView{
            VStack{
                Image(thisDisney.image)
                    .resizable()
                    .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                    .clipped()
                Text(thisDisney.DisneyNameTW)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                Text("上映日期: " + thisDisney.DisneyHours)
                    .font(.caption)
                Spacer()
                Text(thisDisney.DisneyNameUS)
                    .padding(.all, 25)
                    .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                    .cornerRadius(30.0)
                    .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                    .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                Spacer()
                //使用Link的方式, 將youtube預告片的網址放進去
                Link("預告", destination: URL(string: thisDisney.predict)!)
                    .padding(.all,10)
                    .frame(width: 110, height: 45, alignment: .center)
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .font(.system(size: 30, design: .serif))
                    .cornerRadius(20)
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20) //後面留空多少空間
                    .padding(.top, 30)
                    Spacer()
                }
            }
        )
    }
}

```
  <img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/disney.gif">
   </td> 
   </tr>

<tr>
   <td>

```swift
import SwiftUI
//用ScrollView來呈現動漫類的片單

struct Course: Identifiable{
    var id = UUID()
    var image:String
    var courseNameUS:String //故事簡介
    var courseNameTW:String //中文片名
    var courseHours:String //影片類型
    var predict:String //預告片
}

var courses = [
    Course(image: "king", courseNameUS: "「國王排名」是以麾下有名騎士的數量、國民人口、城鎮發展，以及國王本人是否像勇者一樣強大，綜合以上條件來評價各國國王的排行榜。「你想要成為全世界最棒的國王?」伯斯王國的大王子波吉，天生就聽不見、話也說不 好、身體孱弱得舉不起劍，即使如此，他仍然想完成與母親的約定。這樣的堅強與執著也感動了影子一族的卡克， 他決定支持波吉，並成為波吉第一個朋友!但波吉隔天卻怎麼找也找不到卡克。", courseNameTW: "國王排名", courseHours: "類型： 奇幻、冒險、勵志", predict: "https://www.youtube.com/watch?v=aqIJUjTzPbo"),
    Course(image: "spy", courseNameUS: "敘述一名身分為間諜的男性，和另一位實際工作是殺手的女性，以及一個能讀心的超能力者女孩，三人互相隱瞞真實身分所組成的虛假家庭間的家庭喜劇。", courseNameTW: "間諜家家酒", courseHours: "類型： 諜報動作、家庭喜劇", predict: "https://www.youtube.com/watch?v=l1uINfUshjc"),
    Course(image: "war", courseNameUS: "擁有超人般身體能力的男子高中生虎杖悠仁的故事。\n因為某種理由，想要每天17點之前回家的虎杖悠仁來到了不強制出席的靈異現象研究會，享受着悠閒的活動。這樣的某一天，來學校尋找被封印的詛咒之物的青年伏黑惠出現於虎杖的面前。", courseNameTW: "咒術迴戰", courseHours: "類型：  少年漫畫、黑暗奇幻、校園、戰鬥", predict: "https://www.youtube.com/watch?v=QH--l_kJ2lE"),
    Course(image: "kid", courseNameUS: "在演藝圈（這個世界）裏，謊言就是武器。\n在小城市工作的婦產科醫生吾郎，每天都過着與演藝圈無緣的生活。\n另一方面，他“推”的偶像“B小町”的愛開始登上明星之列。如此這般的兩人實現了“最糟糕”的相遇，從此命運的齒輪開始轉動…… ", courseNameTW: "我推的孩子", courseHours: "類型： 懸疑、偶像、戀愛", predict: "https://www.youtube.com/watch?v=ieGJ0CnGkLI"),
    Course(image: "shadow", courseNameUS: "在一個遙遠的地方，居住著一群假裝自己是貴族的人，因為他們沒有臉，必須仰賴被稱為臉的「活人偶」來互相交流，故事描述被稱為艾蜜莉可的臉與她的主人凱特在影宅中的奇妙生活，隨著她們的成長，影宅的神秘與黑暗也逐漸展現出來。", courseNameTW: "影宅", courseHours: "類型：  哥德式、神秘、超自然", predict: "https://www.youtube.com/watch?v=1QPhoqCzU_4"),
]

struct AnimeListView: View {
    @State var showDetialView = false
    @State var selectedAnime: Course?
    var body: some View {
        VStack{
            Text("Anime")
                .padding(.top, 20)
                .foregroundStyle(.secondary)
                .padding(.bottom, 0)
            Text("動漫類")
                .font(.system(size: 40, weight: .bold, design: .rounded))
                .padding(.all, 5)
            ScrollView(.horizontal){
                HStack{
                    ForEach(courses){CourseItem in
                        CardsView(image: CourseItem.image , courseNameUS: CourseItem.courseNameUS, courseNameTW: CourseItem.courseNameTW, courseHours: CourseItem.courseHours)
                            .frame(width: 300) 
                            .onTapGesture {
                                self.showDetialView = true
                                self.selectedAnime = CourseItem
                            }
                    }
                    .sheet(item: self.$selectedAnime, content: {CourseItem in
                        AnimeDetialView(thisAnime: CourseItem)
                    })
                }
            }
        }
    }
}

struct CardsView: View{
    var image:String
    var courseNameUS: String
    var courseNameTW: String
    var courseHours: String
    var body: some View{
        VStack{
            Image(image)
                .resizable()
                .aspectRatio(contentMode: .fit)
            VStack(alignment: .leading, content: {
                Text(courseNameTW)
                    .font(.title)
                    .foregroundStyle(.primary)
                    .lineLimit(3)
                Text(courseHours)
                    .font(.caption)
                    .foregroundStyle(Color(red: 0/255, green: 137/255, blue: 167/255))
            })
            .frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, alignment: .leading)
            .padding(.horizontal, 10)
            .padding(.bottom, 10)
        }
        .background(Color(red: 215/255, green: 240/255, blue: 187/255))
        .clipShape(.rect(cornerRadius: 20))
        .overlay(
            RoundedRectangle(cornerRadius: 20)
                .stroke(Color.gray, lineWidth: 2)
        )
        .padding(.all, 10)
        
    }
}

struct AnimeDetialView: View {
    @Environment(\.presentationMode)
    var presentationMode
    var thisAnime: Course
    var body: some View {
        ScrollView{
            VStack{
                Image(thisAnime.image)
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .clipped()
                Text(thisAnime.courseNameTW)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                Text(thisAnime.courseHours)
                    .font(.caption)
                Spacer()
                Text(thisAnime.courseNameUS)
                    .padding(.all, 25)
                    .background(Color(red: 215/255, green: 240/255, blue: 187/255))
                    .cornerRadius(30.0)
                    .opacity(0.8)
                    .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                Spacer()
                //使用Link的方式, 將youtube預告片的網址放進去
                Link("預告", destination: URL(string: thisAnime.predict)!)
                    .padding(.all,10)
                    .frame(width: 110, height: 45, alignment: .center)
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .font(.system(size: 30, design: .serif))
                    .cornerRadius(20)
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20) //後面留空多少空間
                    .padding(.top, 30)
                    Spacer()
                }
            }
        )
    }
}


```
<img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/anime.gif">
   </td>
   </tr>

<tr>
   <td>

```swift
import SwiftUI
//用HStack和VStack來呈現台灣影視作品

struct Film: Identifiable{
    var id = UUID()
    var image:String
    var filmNameUS:String //故事簡介
    var filmNameTW:String //中文片名
    var filmHours:String //影片類型
    var filmPredict:String //預告片
}

//我把片單兩個兩個存放在三個陣列中，用VStack的方式呈現三組片單
var films = [ //第一組片單
    Film(image: "ghost", filmNameUS: "劇情描述直男警察許光漢，辦案蒐證誤撿地上紅包，被迫成為同志冤鬼林柏宏的冥婚「老公」；人鬼都能冥婚，直男與同志當然也能湊作伙，攜手緝毒追兇，一場荒謬絕倫、笑中帶淚的旅程就此展開。", filmNameTW: "關於我和鬼變成家人的那件事", filmHours: "類型： 奇幻、靈異、LGBT、喜劇", filmPredict: "https://www.youtube.com/watch?v=lQAQpkY4o6U"),
    Film(image: "weird", filmNameUS: "在愛情的世界裡，我們是彼此的怪胎。\n陳柏青是一名嚴重神經性強迫症患者，有非常嚴重的潔癖，非不得已要出門時都是全副武裝；穿防塵衣、戴手套、戴口罩，還會不停的洗手，所以他幾乎沒辦法正常社交生活。 在一般人眼中，柏青就是個異於常人的怪胎。", filmNameTW: "怪胎", filmHours: "類型： 劇情、愛情、浪漫", filmPredict: "https://www.youtube.com/watch?v=byDWAoKEFZ8"),
]

var films1 = [ //第二組片單
    Film(image: "sun", filmNameUS: "講述在駕訓班擔任教練的阿文和琴姐育有兩個兒子，某日，叛逆的小兒子阿和跟好友菜頭進了少年輔育院，而在被害者家屬不斷找阿文求取鉅額賠償之下，阿文受不了總是惹麻煩的阿和，決定將所有希望都託付在大兒子阿豪身上，卻不知道個性善良的資優生心中也藏著不為人知的一面。", filmNameTW: "陽光普照", filmHours: "類型： 犯罪、懸疑、青春", filmPredict: "https://www.youtube.com/watch?v=0bQXpreXRyc"),
    Film(image: "law", filmNameUS: "講述貪財又刻薄、為打贏官司完全沒底線的精算律師─劉浪（陳柏霖 飾），與堅持追求正義、奮發圖強的菜鳥律師─林小顏（郭雪芙 飾），兩人意外成為搭檔，在過程中相互切磋、追尋正義、並碰撞出笑料與火花的喜劇故事。", filmNameTW: "正義的算法", filmHours: "類型： 喜劇、感人、幽默", filmPredict: "https://www.youtube.com/watch?v=1D4xRM492pU"),
]

var films2 = [ //第三組片單
    Film(image: "kill", filmNameUS: "聚焦於1988年台北林森北路條通的一間熱門日式酒店「光」，一群酒店女子在這裡經歷了嫉妒、心碎、友誼與愛情種種百轉千迴的歡場人生。\n 特別是六大金釵的生活，表面五光十色、紙醉金迷，背地裡暗潮洶湧，並因一樁紅鞋無名屍案而被攤在陽光下。", filmNameTW: "華燈初上", filmHours: "類型： 懸疑、寫實、愛情", filmPredict: "https://www.youtube.com/watch?v=a5X_BJFKONU"),
    Film(image: "copy", filmNameUS: "改編自日本推理女王宮部美幸同名暢銷小說，故事描述90年代，一名擅長偵辦兇殺刑案的檢察官郭曉其（吳慷仁飾）面對當時第一起的連續殺人命案，以他心中衡量正義的那把尺對抗連續殺人案兇手，面對辦案過程中兇手不斷的挑釁與隨之擴張的惡，讓曉其決心不惜染髒自己的手，賭上人生也要拖出兇手的犯案證據。", filmNameTW: "模仿犯", filmHours: "類型： 懸疑、犯罪、推理", filmPredict: "https://www.youtube.com/watch?v=Sk-XhCaz5M0"),
]

struct TaiwanListView: View {
    @State var showDetialView = false
    @State var selectedTaiwan: Film?
    var body: some View {
        VStack{
            Text("Taianese films")
                .padding(.top, 20)
                .foregroundStyle(.secondary)
                .padding(.bottom, 0)
            Text("台灣影視作品")
                .font(.system(size: 40, weight: .bold, design: .rounded))
                .padding(.all, 5)
            
            HStack{
                ForEach(films){CourseItem in
                    subCardView(image: CourseItem.image , filmNameUS: CourseItem.filmNameUS, filmNameTW: CourseItem.filmNameTW, filmHours: CourseItem.filmHours)
                        .frame(width: 190) 
                        .onTapGesture {
                            self.showDetialView = true
                            self.selectedTaiwan = CourseItem
                        }
                }
                .sheet(item: self.$selectedTaiwan, content: {CourseItem in
                    TaiwanDetialView(thisAnime: CourseItem)
                })
            }
            HStack{
                ForEach(films1){CourseItem in
                    subCardView(image: CourseItem.image , filmNameUS: CourseItem.filmNameUS, filmNameTW: CourseItem.filmNameTW, filmHours: CourseItem.filmHours)
                        .frame(width: 190) 
                        .onTapGesture {
                            self.showDetialView = true
                            self.selectedTaiwan = CourseItem
                        }
                }
                .sheet(item: self.$selectedTaiwan, content: {CourseItem in
                    TaiwanDetialView(thisAnime: CourseItem)
                })
            }
            HStack{
                ForEach(films2){CourseItem in
                    subCardView(image: CourseItem.image , filmNameUS: CourseItem.filmNameUS, filmNameTW: CourseItem.filmNameTW, filmHours: CourseItem.filmHours)
                        .frame(width: 190) 
                        .onTapGesture {
                            self.showDetialView = true
                            self.selectedTaiwan = CourseItem
                        }
                }
                .sheet(item: self.$selectedTaiwan, content: {CourseItem in
                    TaiwanDetialView(thisAnime: CourseItem)
                })
            }
        }
    }
}

struct subCardView: View{
    var image:String
    var filmNameUS: String
    var filmNameTW: String
    var filmHours: String
    var body: some View{
        VStack{
            Image(image)
                .resizable()
                .aspectRatio(contentMode: .fit)
                .frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, alignment: .leading)
        }
        .background(Color(red: 255/255, green: 204/255, blue: 153/255))
        .clipShape(.rect(cornerRadius: 20))
        .overlay(
            RoundedRectangle(cornerRadius: 20)
                .stroke(Color.gray, lineWidth: 2)
        )
        .padding(.all, 10)
    }
}

struct TaiwanDetialView: View {
    @Environment(\.presentationMode)
    var presentationMode
    var thisAnime: Film
    var body: some View {
        ScrollView{
            VStack{
                Image(thisAnime.image)
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .clipped()
                Text(thisAnime.filmNameTW)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                Text(thisAnime.filmHours)
                    .font(.caption)
                Text(thisAnime.filmNameUS)
                    .padding(.all, 25)
                    .background(Color(red: 254/255, green: 223/255, blue: 225/255))
                    .cornerRadius(30.0)
                    .opacity(0.8)
                    .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                Spacer()
                //使用Link的方式, 將youtube預告片的網址放進去
                Link("預告", destination: URL(string: thisAnime.filmPredict)!)
                    .padding(.all,10)
                    .frame(width: 110, height: 45, alignment: .center)
                    .background(LinearGradient(gradient: Gradient(colors: [Color(red: 255/255, green: 195/255, blue: 0/255), Color(red: 255/255, green: 87/255, blue: 51/255)]), startPoint: .leading, endPoint: .trailing))
                    .foregroundColor(.white)
                    .font(.system(size: 30, design: .serif))
                    .cornerRadius(20)
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName: "chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20) //後面留空多少空間
                    .padding(.top, 30)
                    Spacer()
                }
            }
        )
    }
}
```
  <img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/taiwan.gif">
   </td>
   </tr>

<tr>
   <td>

```swift
import SwiftUI
//使用者可以透過點擊來隨機產生要看哪一部作品

struct TermAndDescription: Identifiable{ //存放片單照片和名稱
    var id = UUID()
    var image:String
    var description:String
}

var myDictionary = [ //存放所有片單的陣列
    TermAndDescription(image: "animal", description: "動物方城市"),
    TermAndDescription(image: "brain", description: "腦筋急轉彎"),
    TermAndDescription(image: "brave", description: "勇敢傳說"),
    TermAndDescription(image: "coco", description: "可可夜總會"),
    TermAndDescription(image: "copy", description: "模仿犯"),
    TermAndDescription(image: "frozen", description: "冰雪奇緣"),
    TermAndDescription(image: "ghost", description: "關於我和鬼變成家人的那件事"),
    TermAndDescription(image: "kid", description: "我推的孩子"),
    TermAndDescription(image: "kill", description: "華燈初上"),
    TermAndDescription(image: "king", description: "國王排名"),
    TermAndDescription(image: "law", description: "正義的算法"),
    TermAndDescription(image: "shadow", description: "影宅"),
    TermAndDescription(image: "spy", description: "間諜家家酒"),
    TermAndDescription(image: "sun", description: "陽光普照"),
    TermAndDescription(image: "war", description: "咒術迴戰"),
    TermAndDescription(image: "weird", description: "怪胎"),
    TermAndDescription(image: "sea", description: "海洋奇緣"),
]

struct CardView: View {
    @State var currentCard = 0
    var body: some View {
        VStack {
            Text("點擊查看今天要看什麼!!")
                .padding(.all, 10)
                .font(.system(size: 25, weight: .bold, design: .rounded))
            VStack{
                Image(myDictionary[currentCard].image)
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                Text(myDictionary[currentCard].description)
                    .font(.system(size: 20, weight: .bold))
                    .foregroundColor(Color(red: 13/255, green: 86/255, blue: 97/255))
                    .padding(.top, 5)
                    .padding(.bottom, 20)
            }
           
            .frame(minWidth: 0, idealWidth: 100, maxWidth: 300, alignment: .leading)
            .background(Color(red: 231/255, green: 209/255, blue: 224/255))
            .clipShape(.rect(cornerRadius: 20))
            .overlay(
                RoundedRectangle(cornerRadius: 20)
                    .stroke(Color.gray, lineWidth: 2)
            )
            .onTapGesture(perform: { //點即時隨機產生id顯示圖片以及片名
                let randomInt = Int.random(in:0...16)
                self.currentCard = randomInt
            })
            
        }.padding(.top, 20)
    }
}


```
<img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/card.gif">
   </td>
   </tr>

<tr>
   <td>

```swift
import SwiftUI
//settings功能是用 @Appstprage 使用者可以輸入姓名，顯示在最上方
//其餘暫無功能

struct SettingView: View {
    let displayFontType = [".default",".rounded",".monospaced",".serif"]
    @State var displayFontSelected = 0
    @State var IsDeepScheme = false;
    @State var colorArray:Array = [255.0,255.0,255.0]
    @State var stepperValue = 0
    @State var sliderValue = 0.0
    @State var date = Date()
    @AppStorage("UserName") var UserName:String = ""
    
    var body: some View {
        NavigationView{
            Form(
                content: {
                    Section(content: {
                        TextField("請輸入您的名字", text: $UserName)
                    }, header: {
                        Text("使用者名稱")
                    })
                    Section(header: Text("字型設定"), content: {
                        Picker(selection: $displayFontSelected, label: Text("字型選擇")){
                            ForEach(0..<displayFontType.count, id: \.self, content:{
                                Text(self.displayFontType[$0])  
                            })
                        }
                    })
                    Section(header: Text("背景風格"), content: {
                        Toggle(isOn: $IsDeepScheme, label: {
                            Text("深色\(String(IsDeepScheme))")
                        })
                    })
                    Section(header: Text("計數器"), content: {
                        Stepper( onIncrement: {stepperValue+=1;}, onDecrement: {stepperValue-=1},
                                 label: {
                            Text("Stepper \(stepperValue)")
                        })
                    })
                    Section(header: Text("滑桿\(sliderValue,specifier: "%.2f")"), content: {
                        Slider(value: $sliderValue, in: 0...1)
                    })
                    Section(header: Text("日期"), content: {
                        DatePicker("\(date.formatted(date: .numeric, time: .omitted))", selection: $date, displayedComponents: [.date])
                    })
                }
            )
            .navigationTitle("Settings 設定")
        }
    }
}

```
  <img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/settings.gif">
   </td>
   </tr>

<tr>
   <td>

```swift
import SwiftUI

//使用Settings中的Stepper，使用者可以透過＋—來記錄自己的完成度，APP會用 @AppStorage來記錄使用者的次數，假如使用者點擊個類別時，整體完成度的數量也會跟著更新。

//每個Row也點進去，點進去後會顯示各種類別的完成比例圖，如果想看整體的完成度，可以點整體完成度，裡面就會有全部以及個類別的完成比例圖。這個部分是用上課所學來發想的。

//完成比例圖和Stepper都是使用 @Appstorage 來存的，所以就算關掉後，還是會有紀錄。

struct type: Identifiable{ //影片種類
    var id = UUID()
    var image:String
    var Name:String
}

var types = [ //片單類別陣列
    type(image: "ghost", Name: "台灣影視作品"),
    type(image: "coco", Name: "迪士尼電影"),
    type(image: "king", Name: "動漫類"),
    type(image: "film", Name: "整體完成度"),
]

struct progressView: View {
    @State var showtypeDetialView = false
    @State var selectedtype: type?
    var body: some View {
        NavigationView{
            List(types){typeItem in
                NavigationLink(
                    destination: typeDetialView(thistype: typeItem), label:{
                        BasicImageRow1(thistype : typeItem)
                    }
                )
            }
            .navigationTitle("片單完成度")
        }
    }
}

struct BasicImageRow1: View {
    //完成比例圖的記錄
    @AppStorage("All") var All:Double = 0.0
    @AppStorage("TWprogress") var TWprogress:Double = 0.0
    @AppStorage("Dprogress") var Dprogress:Double = 0.0
    @AppStorage("Anprogress") var Anprogress:Double = 0.0
    
    //Stepper的記錄
    @AppStorage("ScoreAll") var ScoreAll : Int = 0
    @AppStorage("ScoreTW") var ScoreTW : Int = 0
    @AppStorage("ScoreAS") var ScoreA : Int = 0
    @AppStorage("ScoreDS") var ScoreD : Int = 0
    
    var thistype: type
    
    var body: some View {
        HStack{
            Image(thistype.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thistype.Name)
            Section(content: {
                Stepper( onIncrement: {ScoreAll+=1;All += 0.05885;
                    if(thistype.image == "ghost"){TWprogress+=0.16667;ScoreTW += 1}
                    else if(thistype.image == "coco"){Dprogress+=0.16667;ScoreD += 1}
                    else if(thistype.image == "king"){Anprogress+=0.2;ScoreA += 1}
                    
                }, onDecrement: {ScoreAll-=1;All -= 0.05885;
                    if(thistype.image == "ghost"){TWprogress-=0.16667;ScoreTW -= 1}
                    else if(thistype.image == "coco"){Dprogress-=0.16667;ScoreD -= 1}
                    else if(thistype.image == "king"){Anprogress-=0.2;ScoreA -= 1}
                },
                     label: {
                    if(thistype.image == "ghost"){Text("\(ScoreTW)"+"  部")}
                    else if(thistype.image == "coco"){Text("\(ScoreD)"+"  部")}
                    else if(thistype.image == "king"){Text("\(ScoreA)"+"  部")}
                    else if(thistype.image == "film"){Text("\(ScoreAll)"+"  部")}
                })
            })
            
        }
    }
}

struct typeDetialView: View {
    @AppStorage("All") var All:Double = 0.0
    @AppStorage("TWprogress") var TWprogress:Double = 0.0
    @AppStorage("Dprogress") var Dprogress:Double = 0.0
    @AppStorage("Anprogress") var Anprogress:Double = 0.0
    
    @Environment(\.presentationMode)
    var presentationMode
    var thistype: type
    
    var body: some View {
        ScrollView{
            VStack{
                if(thistype.image == "ghost"){
                    Text("台灣影視作品")
                        .padding(.all, 20)
                        .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                        .cornerRadius(30.0)
                        .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                        .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                    Spacer()
                    Spacer()
                    ZStack{
                        Circle()
                            .stroke(Color(.lightGray), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                        Circle()
                            .trim(from: 0.0, to: TWprogress)
                            .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                            .rotationEffect(Angle(degrees: -90))
                            .overlay(
                                Text("\(Int(TWprogress*100))%")
                                    .font(.system(size: 60))
                                    .bold()
                                    .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                            )
                    }
                }
                else if(thistype.image == "coco"){
                    Text("迪士尼電影")
                        .padding(.all, 20)
                        .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                        .cornerRadius(30.0)
                        .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                        .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                    Spacer() 
                    Spacer()
                    ZStack{
                        Circle()
                            .stroke(Color(.lightGray), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                        Circle()
                            .trim(from: 0, to: Dprogress)
                            .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                            .rotationEffect(Angle(degrees: -90))
                            .overlay(
                                Text("\(Int(Dprogress*100))%")
                                    .font(.system(size: 60))
                                    .bold()
                                    .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                            )
                    }
                }
                else if(thistype.image == "king"){
                    Text("動漫類")
                        .padding(.all, 20)
                        .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                        .cornerRadius(30.0)
                        .opacity(/*@START_MENU_TOKEN@*/0.8/*@END_MENU_TOKEN@*/)
                        .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                    Spacer()
                    Spacer()
                    ZStack{
                        Circle()
                            .stroke(Color(.lightGray), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                        Circle()
                            .trim(from: 0, to: Anprogress)
                            .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 20)
                            .frame(width: 250, height: 250, alignment: .center)
                            .rotationEffect(Angle(degrees: -90))
                            .overlay(
                                Text("\(Int(Anprogress*100))%")
                                    .font(.system(size: 60))
                                    .bold()
                                    .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                            )
                    }
                }
                else if(thistype.image == "film"){
                    HStack{
                        VStack{
                            Text("整體完成度")
                                .padding(.all, 15)
                                .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                                .cornerRadius(30.0)
                                .opacity(0.8)
                                .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                            Spacer()
                            Spacer()
                            ZStack{
                                Circle()
                                    .stroke(Color(.lightGray), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                Circle()
                                    .trim(from: 0, to: All)
                                    .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                    .rotationEffect(Angle(degrees: -90))
                                    .overlay(
                                        Text("\(Int(All*100))%")
                                            .font(.system(size: 50))
                                            .bold()
                                            .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                                    )
                            }
                        }
                        VStack{
                            Text("台灣影視作品")
                                .padding(.all, 15)
                                .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                                .cornerRadius(30.0)
                                .opacity(0.8)
                                .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                            Spacer()
                            Spacer()
                            ZStack{
                                Circle()
                                    .stroke(Color(.lightGray), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                Circle()
                                    .trim(from: 0, to: TWprogress)
                                    .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                    .rotationEffect(Angle(degrees: -90))
                                    .overlay(
                                        Text("\(Int(TWprogress*100))%")
                                            .font(.system(size: 50))
                                            .bold()
                                            .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                                    )
                            }
                        }
                    } 
                    HStack{
                        VStack{
                            Text("迪士尼電影")
                                .padding(.all, 15)
                                .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                                .cornerRadius(30.0)
                                .opacity(0.8)
                                .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                            Spacer()
                            Spacer()
                            ZStack{
                                Circle()
                                    .stroke(Color(.lightGray), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                Circle()
                                    .trim(from: 0, to: Dprogress)
                                    .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                    .rotationEffect(Angle(degrees: -90))
                                    .overlay(
                                        Text("\(Int(Dprogress*100))%")
                                            .font(.system(size: 50))
                                            .bold()
                                            .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                                    )
                            }
                        }
                        VStack{
                            Text("動漫類")
                                .padding(.all, 15)
                                .background(Color(red: 215/255, green: 214/255, blue: 241/255))
                                .cornerRadius(30.0)
                                .opacity(0.8)
                                .frame(minWidth: 0, maxWidth: 350, minHeight: 0, maxHeight: .infinity)
                            Spacer()
                            Spacer()
                            ZStack{
                                Circle()
                                    .stroke(Color(.lightGray), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                Circle()
                                    .trim(from: 0, to: Anprogress)
                                    .stroke(Color(red: 160/255, green: 64/255, blue: 119/255), lineWidth: 15)
                                    .frame(width: 130, height: 130, alignment: .center)
                                    .rotationEffect(Angle(degrees: -90))
                                    .overlay(
                                        Text("\(Int(Anprogress*100))%")
                                            .font(.system(size: 50))
                                            .bold()
                                            .foregroundColor(Color(red: 160/255, green: 64/255, blue: 119/255))
                                    )
                            }
                        }
                    }
                }
            }   
        }
    }
}


```
<img width = "400" src ="https://raw.githubusercontent.com/Rebecca931/yzu-SwiftUI-1103348/main/progress.gif">
   </td>
</tr>
</table>
