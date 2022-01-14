protocol RegexCalculatorProtocol {
    init(pattern: String)
    func calculate(_ string: String) -> Bool
}

struct RegexCalculator {
    private let pattern: String
    
    init(pattern: String) {
        self.pattern = pattern
    }
    
    func calculate(_ string: String) -> Bool {
        do {
            let regex = try NSRegularExpression(pattern: pattern,
                                                options: [])
            let result = regex
                .matches(in: string,
                         options: [],
                         range: NSRange(location: 0,
                                        length: string.count))
                .compactMap { Range($0.range, in: string) }
                .compactMap { String(string[$0]) }
            
            return result.isEmpty ? false : true
        } catch {
            print("\(self) \(error)")
            return false
        }
    }
}
